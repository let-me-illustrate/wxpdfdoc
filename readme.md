# wxPdfDocument - Generation of PDF documents from wxWidgets applications

**wxPdfDocument** allows wxWidgets applications to generate PDF documents.
The code is a port of FPDF - a free PHP class for generating PDF files - to
C++ using the wxWidgets library. Several add-on PHP scripts found
on the FPDF web site are incorporated into wxPdfDocument.

Embedding of PNG, JPEG, GIF and WMF images is supported. In addition to
the 14 standard Adobe fonts it is possible to use other Type1, TrueType
or OpenType fonts - with or without embedding them into the generated
document. CJK fonts are supported, too. Graphics primitives allow the
creation of simple drawings.

- [Installation](#install)
- [Execution of sample applications](#execsamples)
- [Acknowledgements](#acknowledge)

[![Travis](https://img.shields.io/travis/utelle/wxpdfdoc/master.svg?label=Linux+/+OS+X)](https://travis-ci.org/utelle/wxpdfdoc)
 
## <a name="install"></a>Installation

After the release of **wxPdfDocument** version 0.9.5 the build support
has been overhauled. The build files for Windows platforms is now
generated by a (slightly modified) version of [Premake 5](https://premake.github.io/)
(based on Premake 5.0 alpha 11).  

Ready to use project files are provided for Visual C++ 2010, 2012, 2013,
2015, and 2017. Additionally, GNU Makefiles are provided supporting for
example TDM-GCC MinGW.

For Visual Studio 2010+ solutions it is possible to customize the build
by creating a wx_local.props file in the build directory which is used,
if it exists, by the projects. The settings in that file override the
default values for the properties. The typical way to make the file is
to copy wx_setup.props to wx_local.props and then edit local.

For GNU Makefiles the file config.gcc serves the same purpose as the
file wx_setup.props for Visual C++ projects.

The customization files `wx_setup.props` resp. `config.gcc` allow to
customize certain settings like for example the version number and the
root directory of the wxWidgets library.

### wxMSW

When building on Win32 or Win64, you can use the makefiles or one of the
Microsoft Visual Studio solution files in the BUILD folder.

For Visual C++ the debugging properties are set up in such a way that
debugging the sample applications should work right out of the box. For
release builds you may need to copy the wxPdfDocument DLL or add the
`lib` folder path to the Windows search path (PATH environment variable).

### wxGTK

When building on an autoconf-based system (like Linux/GNU-based
systems), the first step is to recreate the configure script doing:

```
  autoreconf
```

Thereafter you should create a

```
  mkdir build-gtk [or any other suitable name]
  cd build-gtk
  ../configure [here you should use the same flags you used to configure wxWidgets]
  make
```
 
Type `../configure --help` for more info.

The autoconf-based system also supports a `make install` target which
builds the library and then copies the headers of the component to
`/usr/local/include` and the lib to `/usr/local/lib` by default, you can use
`pkg-config --cflags` and `--libs` to find the requires compilation and
linking flags in general.

## <a name="execsamples"></a>Executing the sample applications

If you build the **wxPdfDocument** library as a shared object resp. DLL
you have to take different measures on different platforms to execute
the sample applications. The sample applications assume that they are
started from their respective sample directory. If that is not the case,
command line options are available to set the working directory and the
path to the font directory of **wxPdfDocument** (`lib/fonts`).

### wxMSW

Copy the wxPdfDocument DLL to the samples' directories or change the PATH
environment variable appropriately. Set environment variable `WXPDF_FONTPATH`:

```
set WXPDF_FONTPATH=<wxPdfDocument-path>\lib\fonts
```

### wxGTK

Set environment variables before starting the applications, i.e.

```
LD_LIBRARY_PATH=<wxPdfDocument>/lib:$LD_LIBRARY_PATH WXPDF_FONTPATH=<wxPdfDocument>/lib/fonts ./application
```

### wxMAC

You should set environment variable `WXPDF_FONTPATH`:

```
WXPDF_FONTPATH=<wxPdfDocument>/lib/fonts
```

If **wxPdfDocument** has been built as a shared object you have to make it accessible,
for example by copying it to `/usr/local/lib`.

## <a name="acknowledge"></a>Acknowledgements

I'm very grateful to Bruno Lowagie, the main author of the [iText Java library](http://itextpdf.com/),
for allowing to take lots of ideas and inspirations from this great Java PDF library.
Especially the font handling and font subsetting was influenced in that way.

Many thanks go to Ben Moores who provided code for layers and patterns he
wrote for his PDF extension for Mapnik (http://www.mapnik.org). This code
has been extended based on ideas from the iText Java library and was
incorporated into wxPdfDocument.

Support for Indic scripts is based on the efforts of Ian Back, creator of
the PHP library [mPDF](http://www.mpdf1.com/mpdf/index.php); special thanks to K Vinod Kumar
of the [Centre for Development of Advanced Computing, Mumbai](http://cdac.in/),
for clearing license issues of the Raghu font series.

Kudos to Mark Dootson for contributing major enhancements of wxPdfDC and
it's integration into the wxWidgets printing framework.

Thanks to one of the wxWidgets core developers, Vadim Zeitlin, the build system
could be overhauled and continuous integration could be added.

Since wxPdfDocument is based on the great FPDF PHP class and several of the
contributions to it found on the [FPDF website](http://www.fpdf.org) I would
like to thank 

- Olivier Plathey (FPDF, Barcodes, Bookmarks, Rotation),
- Maxime Delorme (Sector)
- Johannes Guentert (JavaScript)
- Martin Hall-May (WMF images, Transparency)
- Emmanuel Havet (Code39 barcodes)
- Shailesh Humbad (POSTNET barcodes)
- Matthias Lau (i25 barcodes)
- Pierre Marletta (Diagrams)
- Laurent Passebecq (Labels)
- David Hernandez Sanz (additional graphics primitives)
- Valentin Schmidt (Transparency, Alpha channel)
- Jan Slabon (FPDI)
- Klemen Vodopivec (Protection)
- Moritz Wagner (Transformation)
- Andreas Wuermser (Clipping, Gradients, Transformation)
