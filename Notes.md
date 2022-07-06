# Tools Installation
[Angular, Node Installation](https://github.com/darbyluv2code/fullstack-angular-and-springboot/blob/master/install-angular-tools/mac/install-mac.md)

# Definitions

Traditional Application:
Each user action results in a full HTML page load

Single Page Application
Partial Update instead of full page load on user actions, e.g. google maps, gmails

**Angular** is a framework for building modern single-page applications, e.g., Citi Bank, MSBox (www.madewithangular.com)

## Install Maven
- Download from [official site](https://maven.apache.org/download.cgi) (Download `Binary tar.gz archive` version)
- Unzip and put unzipped folder to `usr/local` folder
- Open zshrc file with `code ~/.zshrc` (or `vim ~/.zshrc`)
- Add following code to `.zshrc` file:
```
#Maven
export M2_HOME=/usr/local/apache-maven-3.8.6
export M2=$M2_HOME/bin
export PATH=$M2:$PATH
```
- save, enter `source ~/.zshrc` in terminal
- test installation with `mvn -v`
- Reference: [this](https://icode.best/i/26862246930204) or [this](https://cloud.tencent.com/developer/article/1680711)
