# Mobile PDFium

[![Build Status](https://travis-ci.com/prsolucoes/mobile-pdfium.svg?branch=master)](https://travis-ci.com/prsolucoes/mobile-pdfium)

This project compile PDFium to mobile platforms. Current project compiles to:  

- [x] iOS device
- [x] iOS simulator
- [x] macOS
- [ ] Android

## Requirements

1. ninja (brew install ninja)  
2. python3  
3. pip (generally called pip3 for python3)  

## How to compile (general)

1. Get the source:  
```git clone https://github.com/prsolucoes/mobile-pdfium.git```  

2. Install pip requirements:  
```pip3 install -r requirements.txt``` 
or  
```pip3 install -r requirements.txt --user``` 

3. Get Google Depot Tools:  
```python3 make.py run build-depot-tools```  
```export PATH=$PATH:$PWD/depot-tools```  

4. Get PDFium:  
```python3 make.py run build-pdfium```  

Obs:
- The file **make.py** need be executed with python3.  
- These steps you only need make one time.  
- If you change **pdfium** git commit revision on file **make.py** only execute step 4.

## How to compile for iOS

1. Execute all **general** steps

2. Apply patchs:  
```python3 make.py run apply-patch-ios```  

3. Compile:  
```python3 make.py run build-ios```  
  
4. Install libraries:  
```python3 make.py run install-ios```  

5. Check generated file:  
```file build/ios/release/libpdfium.a```  

Obs:
- The file **make.py** need be executed with python3.  

## How to compile for macOS

1. Execute all **general** steps

2. Apply patchs:  
```python3 make.py run apply-patch-macos```  

3. Compile:  
```python3 make.py run build-macos```  
  
4. Install libraries:  
```python3 make.py run install-macos```  

5. Check generated file:  
```file build/macos/release/libpdfium.a```  

6. Run sample (optional):  
```python3 make.py run sample```  

Obs:
- The file **make.py** need be executed with python3.  

## Prebuilt binary

You can download a prebuilt copy here:  
https://www.dropbox.com/s/mp44ymlxza1gaga/libpdfium-2019-11-28.a?dl=1

## How to include files and extend pdfium

Check tutorial here: [How to include files](HOW_TO_INCLUDE_FILES.md)

## Generate patch and diff

To generate diff follow the steps:

1. Modify the file that you need from the **pdfium** project.
2. Copy the file to **"patch"** folder with **"_modified"** suffix.
3. Revert the changes of pdfium changed file using command `git checkout filename.extension`.
4. Generate diff between the original file and copied file with command `git diff -u filename.extension <root-folder>/patchs/filename_modified.extension > <root-folder>/patchs/filename.patch`.
5. Add more one line on iOS or macOS patch command calls inside file **"make.py"**.
6. Apply patchs executing `python3 make.py run apply-patch-ios` or `python3 make.py run apply-patch-macos`.
