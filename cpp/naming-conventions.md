<!-- TITLE: C++ Naming Conventions -->
<!-- SUBTITLE: A quick summary of Naming Conventions -->

# Casing
Public and private functions and local variables are in lowerCamelCase.

```c_cpp
bool playVideo(int fileIndex);
```

Namespaces are in lowercase with underscore separation.

```c_cpp
namespace sev_lite { }
```

Definitions are in uppercase with underscore separation, and are prefixed with the namespace in uppercase.

```c_cpp
#define SEV_LITE_OPTION_ENABLED
```

Header guards are in uppercase with underscore separation, are prefixed with the namespace in uppercase, followed by the filename in uppercase, and ended with an \_H suffix. The statements #else and #endif must be followed by a C-style comment of the original #if statement.

```c_cpp
#ifndef SEV_LITE_EVENT_LOOP_HOOP_H
#define SEV_LITE_EVENT_LOOP_HOOP_H
#endif /* #ifndef SEV_LITE_EVENT_LOOP_HOOP_H */
```

Class and struct names are UpperCamelCase. Pure virtual interface classes start with `I` prefix.

```c_cpp
class PlayerController { };
class IStream { };
struct Point { };
```

Private member variables are prefixed with `m\_`, global variables with `g\_`, static and anonymous namespace variables with `s\_`, non-local static const variables with `c\_`. Camel case following an underscore always continues with \_UpperCamelCase.

```c_cpp
class PlayerController
{
private:
	Point m_Position;
	
};
```

Public member variables are in UpperCamelCase without prefix.

```c_cpp
struct Point
{
public:
	float X, Y;
	
};
```

File names should match the class name or function name and must be in lowercase with underscore separation. Include statements must always use `<...>` for code outside of the project. For third party includes, the capitalization of the file name must match the original third party capitalization.

```c_cpp
#include <string>
#include "player_controller.h"
```

Exposed C-style interfaces of functions start with the namespace in uppercase optionally followed by the classname in UpperCamelCase without modification, and then followed by the function name in lowerCamelCase without modification.

```c_cpp
crc32_t SEV_crc32(const char *str);
SEV_EventLoop *SEV_EventLoop_new();
void *SEV_EventLoop_run(SEV_EventLoop *eventLoop);
```

# Abbreviations
Common abbreviations should not be fully capitalized. Likewise, abbreviations should not be separated by underscores either.

```c_cpp
void setIoBuffer(IoBuffer *ioBuffer); // Correct for a class referring to an IO Buffer
void setIOBuffer(IOBuffer *iOBuffer); // This would be an interface class referring to an O Buffer
#include <io_buffer.h> // IO Buffer class
#include <i_o_buffer.h> // O Buffer interface
```

# Tabs and spaces
Use tabs for indentation and spaces for alignment. Tabs may be either 2, 4 or 8 spaces, it does not really matter. When aligning, the aligned parts must use the same number of tabs.

```
enum░class░Color
{
▓▓▓▓Blue░░░░░░=░1;
▓▓▓▓Turquoise░=░2;
};
```

# Getters and setters
Variable names must not be verbs. Do not include `get` as part of the getter function name. Note that while "size" can technically be used as a verb, it is not commonly used as such in programming, as the verb "resize" is more commonly used for such operation. Depending on the context this may vary.

```c_cpp
size_t size();
void setSize(size_t size);
```

# Booleans
Boolean variable names and functions that calculate a boolean must not be verbs, but may be past tense verbes. This in order to avoid getters that sound like functions. Names must also not imply another variable type. Functions which merely return a boolean as success result do not apply to this rule.

```c_cpp
bool m_CallParent; // Not okay. Getter will conflict with function bool callParent()
bool m_ParentCalled; // Okay, but ambigious whether a return status or an expectation
bool m_PlayVideo; // Not okay. Getter will conflict with function bool playVideo()
bool m_VideoPlayed; // Okay, but ambigious whether a return status or an expectation
bool m_PlayedVideo; // Okay, but ambigious whether a return status or an expectation
bool m_Rectangular; // Okay
bool m_Rectangle; // Not okay, implies a Rectangle type rather than a bool
```

The following verbs: `is`, `must`, `can`, `will`, `has`, and `should`, however, are allowed and recommended only for booleans, and functions that return boolean variables. These should therefore, also not be used for non-boolean returning functions or variables. Verbs should be omitted if there is no chance for ambiguity.

```c_cpp
bool m_HasCalledParent; // Okay
bool m_ShouldCallParent; // Okay
bool m_MustCallParent; // Okay
bool m_IsRectangular; // Okay, but prefer m_Rectangular
bool m_IsRectangle; // Okay
```

Choosing between having an object or verb is first, depends on the context.

```c_cpp
bool m_ShouldPlayVideo;
bool m_ShouldPlayAudio;
bool m_ShouldPlayGame;

bool m_HasVideoPlayed;
bool m_HasVideoPaused;
bool m_HasVideoStopped;
```

# Enumerations
Enumerations should have singular name. Bit field enumerations should end with `Options`, `Flags`, `Mask`, or any other non-ambigious name.

```c_cpp
enum class Color;
enum class RuntimeOptions;
enum class RenderFlags;
```

(This should be part of structure conventions page.) Enumerations should always be specified as `enum class` in the namespace scope when publicly used. Private enums may be specified as `enum` within the class scope.

```c_cpp
enum class Color
{
	Red,
	Green,
	Blue
};
```
# Bit field enumerations
(This should be part of structure conventions page. Or rename to style conventions, with subtitle naming and structure conventions.) Bit field enumerations should provide their own operators as needed.

```c_cpp
#include <type_traits>

enum class ColorMask
{
	Red =   1 << 1,
	Green = 1 << 2,
	Blue =  1 << 3
};

inline ColorMask operator | (const ColorMask l, const ColorMask r)
{
    return (ColorMask)(static_cast<const std::underlying_type<ColorMask>>(l)
		 | static_cast<const std::underlying_type<ColorMask>>(r));
}
```