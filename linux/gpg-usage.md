# Gpg使用指南

**mac下安装gpg**

```
brew install gpg
```


**生成秘钥对**

```
gpg --gen-key
```

**导出公钥**

```
gpg --export --armor keyID > gpgkey.pub.asc
```

**上传公钥**

```
gpg --keyserver keyserverAddress --send mykeyID
```

**search**

```
gpg --keyserver keyserver.ubuntu.com --serach-keys rikulu
```

**导入**

```
gpg --import gpgkey.pub.asc
gpg --keyserver keyserverAddress --recv-keys pubkeyID
```

# 加密解密

```
gpg -e -r username filename
gpg -d filename.gpg
```

# 签名

```
gpg -o doc.sig -s doc
```
