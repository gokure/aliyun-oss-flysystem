# Aliyun OSS Flysystem

💾 Flysystem Adapter for [Aliyun Object Storage Service](http://oss.aliyun.com).

[![Latest Stable Version](https://poser.pugx.org/alphasnow/aliyun-oss-flysystem/v/stable)](https://packagist.org/packages/alphasnow/aliyun-oss-flysystem)
[![Total Downloads](https://poser.pugx.org/alphasnow/aliyun-oss-flysystem/downloads)](https://packagist.org/packages/alphasnow/aliyun-oss-flysystem)
[![Code Coverage](https://scrutinizer-ci.com/g/alphasnow/aliyun-oss-flysystem/badges/coverage.png?b=master)](https://scrutinizer-ci.com/g/alphasnow/aliyun-oss-flysystem/?branch=master)
[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/alphasnow/aliyun-oss-flysystem/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/alphasnow/aliyun-oss-flysystem/?branch=master)
[![License](https://poser.pugx.org/alphasnow/aliyun-oss-flysystem/license)](https://packagist.org/packages/alphasnow/aliyun-oss-flysystem)
[![FOSSA Status](https://app.fossa.com/api/projects/git%2Bgithub.com%2Falphasnow%2Faliyun-oss-flysystem.svg?type=shield)](https://app.fossa.com/projects/git%2Bgithub.com%2Falphasnow%2Faliyun-oss-flysystem?ref=badge_shield)
[![Build Status](https://github.com/alphasnow/aliyun-oss-flysystem/workflows/CI/badge.svg)](https://github.com/alphasnow/aliyun-oss-flysystem/actions)

## Compatibility

| **php**  | **flysystem**  |  **aliyun-oss-flysystem** | **document**
|---|---|---|---|
|>=5.5.9,\<7.0| ~1.0.0  | ^0.3  | [readme](https://github.com/alphasnow/aliyun-oss-flysystem/blob/0.x/README.md) |
|>=7.0| ^1.0 | ^1.0  | [readme](https://github.com/alphasnow/aliyun-oss-flysystem/blob/1.x/README.md) |
|>=8.0| ^3.0 | ^3.0  | [readme](https://github.com/alphasnow/aliyun-oss-flysystem/blob/master/README.md)

## Installation

```bash
composer require "alphasnow/aliyun-oss-flysystem"
```

## Usage

### Initialize
```php
use OSS\OssClient;
use AlphaSnow\Flysystem\Aliyun\AliyunFactory;

$config = [
    "access_key_id" => "**************",             // Required, YourAccessKeyId
    "access_key_secret" => "********************",   // Required, YourAccessKeySecret
    "endpoint" => "oss-cn-shanghai.aliyuncs.com",    // Required, Endpoint
    "bucket" => "bucket-name",                       // Required, Bucket
];

$flysystem = (new AliyunFactory())->createFilesystem($config);

$flysystem->write('file.md', 'contents');
$flysystem->writeStream('foo.md', fopen('file.md', 'r'));

$fileExists = $flysystem->fileExists('foo.md');
$flysystem->copy('foo.md', 'baz.md');
$flysystem->move('baz.md', 'bar.md');
$flysystem->delete('bar.md');
$has = $flysystem->has('bar.md');

$read = $flysystem->read('file.md');
$readStream = $flysystem->readStream('file.md');

$flysystem->createDirectory('foo/');
$directoryExists = $flysystem->directoryExists('foo/');
$flysystem->deleteDirectory('foo/');

$listContents = $flysystem->listContents('/', true);
$listPaths = [];
foreach ($listContents as $listContent) {
    $listPaths[] = $listContent->path();
}

$lastModified = $flysystem->lastModified('file.md');
$fileSize = $flysystem->fileSize('file.md');
$mimeType = $flysystem->mimeType('file.md');

$flysystem->setVisibility('file.md', 'private');
$visibility = $flysystem->visibility('file.md');
```

### Options
```php
$flysystem->write('file.md', 'contents', [
    "options" => [OssClient::OSS_CHECK_MD5 => false]
]);
$flysystem->write('bar.md', 'contents', [
    "headers" => ["Content-Disposition" => "attachment; filename=file.md"]
]);
$flysystem->write('baz.md', 'contents', [
    "visibility" => "private"
]);
```

## Reference
[https://github.com/thephpleague/flysystem](https://github.com/thephpleague/flysystem)   

## License
The MIT License (MIT). Please see [License File](LICENSE) for more information.

[![FOSSA Status](https://app.fossa.com/api/projects/git%2Bgithub.com%2Falphasnow%2Faliyun-oss-flysystem.svg?type=large)](https://app.fossa.com/projects/git%2Bgithub.com%2Falphasnow%2Faliyun-oss-flysystem?ref=badge_large)
