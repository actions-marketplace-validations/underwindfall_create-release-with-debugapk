# create-release-with-debugapk

## Example Usage

```yaml
name: CI

on:
  push:
    branches: 
      - master

jobs:

  build:

    runs-on: ubuntu-18.04


    steps:

    - uses: actions/checkout@v2
      
    - name: Use Java8
      uses: actions/setup-java@v1
      with:
          java-version: 1.8

    - name: Build debug apk
      run: ./gradlew clean assembleDebug

    - name: Create release and upload apk
      uses: underwindfall/create-release-with-debugapk@V0.0.4
      env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
      with:
        tag_name: v1.0.0
        upload_url: ${{ steps.create_release.outputs.upload_url }}
        asset_path: app/build/outputs/apk/debug/app-debug.apk
        asset_name: Example.apk
        asset_content_type: application/zip
```