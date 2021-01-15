# SentencePiece Java Wrapper

![Build](https://github.com/levyfan/sentencepiece-jni/workflows/Build/badge.svg)

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

## Using sentencepiece-jni as a dependency

Because the resulting JAR is platform-dependent, resolving this dependency is managed by the [os-maven-plugin](https://github.com/trustin/os-maven-plugin). Follow the instructions there to use this platform-dependent JAR.

Please note you need to have a C++ compiler and cmake installed.

## Usage

See [SentencePieceProcessorTest](src/test/java/com/github/google/sentencepiece/SentencePieceProcessorTest.java) for more.
