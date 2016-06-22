# Utf8Ucs2Converter
C++ methods for converting between UTF-8 std::string and UCS-2 std::wstring (c++98 compatible)

If you want to convert a UTF-8 string into UCS-2 and/or vice versa with a C++98 compiler (so no C++11 or better is available),
this code will do the word with little prerequisites. Please note that boost utf_to_utf() is not suitable for UTF-8 from/to
UCS-2 conversion because it converts to/from UTF-8 to/from UTF-16 which is a different encoding.

## Supported string formats:
UTF-8: A bytestream where 1 or more bytes encode one particular glyph.

UCS-2: A 2-bytestream where exactly 2-bytes encode one particular glyph. (This is often found in a wchar_t/wstring)

## Unsupported string formats:
UTF-16: A bytestream where 2 or more (!) bytes encode one particular glyph.

UCS-4: Same as UCS-2, but 4 bytes per glyph. UCS-2 cannot hold the full range of UTF-8 (or UTF-16) glyphs. But UCS-4 can.

## C++11
As said above this code becomes obsolete in C++11 and something like the following should be used instead.

\#include <locale>

\#include <codecvt>

std::string wstringToUtf8(const std::wstring& str)

{

	std::wstring_convert<std::codecvt_utf8<wchar_t>> strCnv;

	return strCnv.to_bytes(str);

}


std::wstring utf8ToWstring(const std::string& str)

{

	std::wstring_convert< std::codecvt_utf8<wchar_t> > strCnv;

	return strCnv.from_bytes(str);

}
