# TAP-14-demo

## Setup

using https://github.com/vmware-labs/repository-editor-for-tuf
a fake breaking change is available at:  https://github.com/mnm678/tuf/tree/tap14-test


## Demo

### Make initial repository
```
mkdir repo && cd repo
git init .
echo "privkeys.json" > .gitignore
tufrepo init
git commit -a -m "initial top-level metadata"
```

### make v2 repo
```
install fake breaking change
mkdir 2 && cd 2
git init .
echo "privkeys.json" > .gitignore
tufrepo init
git commit -a -m "initial top-level metadata"
```

### 2 has the breaking change
```
cat 1.targets.json | jq
cat ../1.targets.json | jq
```

### add a file to both
```
mkdir targets
mkdir targets/files
vim targets/files/file1.txt
cp -r targets ../
```
add text
```
tufrepo add-target files/file1.txt targets/files/file1.txt
tufrepo snapshot
```

```
cd ..
```
install v1 tuf
```
tufrepo add-target files/file1.txt targets/files/file1.txt
tufrepo snapshot

cat 2.targets.json | jq
cat 2/2.targets.json | jq
```
