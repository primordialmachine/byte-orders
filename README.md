# Primordial Machine's Byte Order Library
C++ 17 library providing Byte order detection. 
The library is made available publicly on [GitHub](https://github.com/primordialmachine/byte-order) under the [MIT License](https://github.com/primordialmachine/byte-order/blob/master/LICENSE),

## Restrictions
*The library officially only supports Visual Studio 2017.*

## Usage Example
To determine target environment's Byte order, evaluate the constant expression function `get_byte_order`, which returns an enum class element from the `byte_order` enum class.
```
#include "primordialmachine/byte_order/include.hpp"
#include <stdlib.h>

int main(int argc, char **argv) {
  using namespace primordialmachine;
  switch (get_byte_order()) {
    case byte_order::little_endian:
      {
        std:cout << "Environment Byte order is Little Endian" << std::endl; 
        return EXIT_SUCCESS;
      } break;
    case byte_order::big_endian:
      {
        std::cout << "Environment Byte order is Big Endian" << std::endl;
        return EXIT_SUCCESS;
      } break;
    default:
     {
        // This code should never be reached as the Byte order is determined
        // at compile time. That is, if the library fails to determine the
        // Byte order, it will raise a compile-time error.
        std::err << "unable to determine Environment Byte order" << std::endl;
        return EXIT_FAILURE;
     }
  };
}
```
If the Byte order can not be determined by the constant expression, a compile-time error is raised.

## Creating the library with Visual Studio 2017
- Open the solution `byte-order.sln` in Microsoft Visual Studio 2017.
- Batch build everything.
- The folder `packages` contains the distribution of the library i.e. include files and the static libraries for
  - the platforms `Win32` and `x64` and
   - configurations `Release` and `Debug`.
- Copy the contents of the `packages` folder into a directory. Let `[library home]` be a placeholder denoting the path by which that folder can be referenced from your project. 
- Add
  - the include path `[library home]/primordialmachine/byte-order/${Platform.toLower()}/{Configuration.toLower()}/includes` and
  - the library path `[library home]/primordialmachine/byte-order/${Platform.toLower()}/{Configuration.toLower()}/libraries` to your project.
- Link your project with the library `byte-order.lib`.
- Add the include directive `#include "primordialmachine/byte_order/include.hpp"` where appropriate.
- You can now use the functionality provided by the library.

## Library Interface Documentation
## `namespace primordialmachine`
The namespace this library is adding its declarations/definitions to.
The added namespace elements are documented below.
#### `enum class byte_order { ... }`
An enum class of the Byte orders known to this library.
The contained enum class elements are documented below.
- `little_endian`: enum class element denoting Little Endian Byte order.
- `big_endian` enum class element denoting Big Endian Byte order.

#### `byte_order get_byte_order()`
A constant expression function getting the target environment's Byte order. It has zero parameters and returns a value of type `byte_order` which denotes the target environment's Byte order. If the Byte order can not be determined, a compile-time error is raised.
