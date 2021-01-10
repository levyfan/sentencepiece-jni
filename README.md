# SentencePiece Java Wrapper

[![Build Status](https://travis-ci.org/levyfan/sentencepiece-jni.svg?branch=master)](https://travis-ci.org/levyfan/sentencepiece-jni)

Java wrapper for [SentencePiece](https://github.com/google/sentencepiece) with JNI. This module wraps 
`sentencepiece::SentencePieceProcessor` class with the following modifications:

* Encode and Decode methods are re-defined as EncodeAsIds, EncodeAsPieces, DecodeIds and DecodePieces respectively.
* SentencePieceText proto is not supported.

## SentencePiece Version

[v0.1.92](https://github.com/google/sentencepiece/releases/tag/v0.1.92)

## Build and Install SentencePiece

To build and install the Java wrapper from source, please try the following commands:

```bash
% mvn clean install
```

If you're trying to build on Windows, you need to specify the Windows-compatible pom file:

```bash
% mvn -f pom-windows.xml clean install
```

Please note you need to have a C++ compiler and cmake installed.

## Usage

See [SentencePieceProcessorTest](src/test/java/com/github/google/sentencepiece/SentencePieceProcessorTest.java) for more.
