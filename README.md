Building Equinox
----------------

You need to have the Haskell MiniSat binding installed to build
Equinox. The following commands should work:

```
cabal update
cabal install minisat
make
```

Installation Instructions on Mac OS X (10.10.+)
-----------------------------------------------
The following scripts are **unmodified** from the original source; this repo is meant as a **backup** of a working version, along with any associated instructions to help users get this running on their Macs.

1. Clone the equinox project from Github or download the zip.
2. Download Haskell from the official site -- I used the installer, but you could do it with homebrew as well. **I think you can avoid all the problems I had (see below @ step 12) if you download the Full version of Haskell, not Core, but I'm not sure.  I only used Core because I wanted to save hard drive space... (oops)

https://www.haskell.org/platform/mac.html#osx-none

3. Install Haskell and follow the prompts if using the installer.

4. In Terminal, check to see if it installed properly by typing:
```bash
    cabal --v
```
5.  It might download something from haskell.org... just let it do its own thing

6.  Append the path to Haskell to your PATH:
```bash
    export PATH="$HOME/Library/Haskell/bin:$PATH"
```
7.  Update cabal to the latest version
```bash
    cabal update
```
8.  Install minisat (might take a while)
```bash
    cabal install minisat
```
9.  Go to the folder where you've placed equinox

10.  Inside the equinox folder, you will need to compile everything via the make command
```bash
    make
```
11.  If you only get warnings (in purple text in Terminal), you can ignore them.

12.  If you're missing the packages (red text in Terminal), you will need to install them manually (this is where trial and error happened for me...):
* Could not find module ‘Control.Monad.State’
```bash
     cabal install mtl
```
* Could not find module ‘System.Random’
```bash
     cabal install random
```
* Could not find module ‘Test.QuickCheck’
```bash
     cabal install QuickCheck
```
* Could not find module ‘System.Time’
```bash
     cabal install old-time-1.1.0.3
```
13.  Update your package cache for cabal
```bash
    sudo ghc-pkg recache
```
14.  Finally, run paradox in Terminal:
```bash
    ./paradox tptp_file
```
e.g., I dumped some TPTP files in the Problems folder with the model flag and it will print the model in Terminal for me:
```bash
    ./paradox Problems/most.tptp --model
```
![paradox](/images/2018-04-18_09-52-38.jpg?raw=true)
You can use the > command to print models to a file.
```bash
    ./paradox Problems/most.tptp --model --verbose 2 > Problems/most_output.txt
```
![paradoxoutput](/images/2018-04-18_09-59-29.jpg?raw=true)
