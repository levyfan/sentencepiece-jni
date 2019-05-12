# SentencePiece Java Wrapper

Java wrapper for [SentencePiece](https://github.com/google/sentencepiece) with JNI. This module wraps 
`sentencepiece::SentencePieceProcessor` class with the following modifications:

* Encode and Decode methods are re-defined as EncodeAsIds, EncodeAsPieces, DecodeIds and DecodePieces respectively.
* SentencePieceText proto is not supported.

## Build and Install SentencePiece

To build and install the Java wrapper from source, please try the following commands:

```bash
% mvn clean install
```

## Usage

See [SentencePieceProcessorTest](src/test/java/com/github/google/sentencepiece/SentencePieceProcessorTest.java) for more.
