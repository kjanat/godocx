# GoDocx

[![Go CI](https://github.com/kjanat/godocx/actions/workflows/go.yml/badge.svg)][ci]
![GitHub go.mod Go version](https://img.shields.io/github/go-mod/go-version/kjanat/godocx)
[![Go Reference](https://pkg.go.dev/badge/github.com/kjanat/godocx.svg)][go.dev godocx]
[![Go Report Card](https://goreportcard.com/badge/github.com/kjanat/godocx)][goreportcard]
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)][oss-mit-license]

<p align="center"><img width="650" src="./godocx.png" alt="GoDocx logo"></p>

GoDocx is a library written in pure Go providing a set of functions that allow you to write to and read from Docx file.

This library needs Go version 1.18 or later. The usage documentation for the GoDocx can be accessed via the [GoDocx Documentation Page][pages].

In depth, go docs can be seen using go's built-in documentation tool, or online at [go.dev][go.dev godocx]. Please refer the [subpackage docx][go.dev godocx/docx] for the list of functions that can be used.

## Usage

Here's a simple example of how you can use GoDocx to create and modify DOCX documents:

## Installation

Use the GoDocx in your project

```bash
go get github.com/kjanat/godocx
```

### Examples

Explore additional examples and use cases over at the [gomutex/godocx-examples][godocx-examples] GitHub repository dedicated to showcasing the capabilities of Golang Docx.

```go
// More examples in separate repository
// https://github.com/gomutex/godocx-examples

package main

import (
    "log"

    "github.com/kjanat/godocx"
)

func main() {
    // Open an existing DOCX document
    // document, err := godocx.OpenDocument("./testdata/test.docx")

    // Create New Document
    document, err := godocx.NewDocument()
    if err != nil {
        log.Fatal(err)
    }

    document.AddHeading("Document Title", 0)

    // Add a new paragraph to the document
    p := document.AddParagraph("A plain paragraph having some ")
    p.AddText("bold").Bold(true)
    p.AddText(" and some ")
    p.AddText("italic.").Italic(true)

    document.AddHeading("Heading, level 1", 1)
    document.AddParagraph("Intense quote").Style("Intense Quote")
    document.AddParagraph("first item in unordered list").Style("List Bullet")
    document.AddParagraph("first item in ordered list").Style("List Number")

    records := []struct{ Qty, ID, Desc string }{{"5", "A001", "Laptop"}, {"10", "B202", "Smartphone"}, {"2", "E505", "Smartwatch"}}

    table := document.AddTable()
    table.Style("LightList-Accent4")
    hdrRow := table.AddRow()
    hdrRow.AddCell().AddParagraph("Qty")
    hdrRow.AddCell().AddParagraph("ID")
    hdrRow.AddCell().AddParagraph("Description")

    for _, record := range records {
        row := table.AddRow()
        row.AddCell().AddParagraph(record.Qty)
        row.AddCell().AddParagraph(record.ID)
        row.AddCell().AddParagraph(record.Desc)
    }

    // Save the modified document to a new file
    err = document.SaveTo("demo.docx")
    if err != nil {
        log.Fatal(err)
    }
}
```

## Demo Output

This is screenshot of demo document generated from the GoDocx library.

![Screenshot of the demo output](https://github.com/gomutex/godocx-examples/raw/main/demo.png)

## Feature addition request

If you need a feature that's missing in GoDocx, feel free to raise an issue
describing what you want to achieve, along with a sample `DOCX`.
While I can't promise immediate implementation, I'll
review your request and work on it if it's valid.

## Inspiration

The GoDocx library is inspired from [python-openxml/python-docx][python-openxml/python-docx].

## Licenses

The GoDocx library is licensed under the [MIT License][oss-mit-license].

<!-- Markdown link definitions -->
[ci]: https://github.com/kjanat/godocx/actions/workflows/go.yml
[go.dev godocx]: https://pkg.go.dev/github.com/kjanat/godocx
[go.dev godocx/docx]: https://pkg.go.dev/github.com/kjanat/godocx/docx
[godocx-examples]: https://github.com/gomutex/godocx-examples
[goreportcard]: https://goreportcard.com/report/github.com/kjanat/godocx
[oss-mit-license]: https://opensource.org/licenses/MIT
[pages]: https://kjanat.github.io/godocx
[python-openxml/python-docx]: https://github.com/python-openxml/python-docx
