name: Build Windows EXE
on: [workflow_dispatch]

jobs:
  build:
    runs-on: windows-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v5
        with:
          python-version: '3.11'
      - run: pip install pyinstaller
      - shell: pwsh
        run: |
          $script = Get-ChildItem -File | Where-Object { $_.Extension -in '.py', '.pyw' } | Select-Object -First 1
          if (-not $script) {
            Write-Error "Repository mein koi .py ya .pyw file nahi mili!"
            exit 1
          }
          Write-Host "Building EXE from: $($script.Name)"
          pyinstaller --onefile --windowed --name "FB_Profile_Manager" $script.FullName
      - uses: actions/upload-artifact@v4
        with:
          name: FB_Profile_Manager_EXE
          path: dist/FB_Profile_Manager.exe
