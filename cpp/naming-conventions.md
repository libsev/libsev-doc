<!-- TITLE: C++ Naming Conventions -->
<!-- SUBTITLE: A quick summary of Naming Conventions -->

# C++ Naming Conventions
# Getters and setters
Variable names must not be verbs. Do not include `get` as part of the getter function name.

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

The following verbs: `is`, `must`, `can`, `will`, `has`, and `should`, however, are allowed and recommended only for booleans, and functions that return boolean variables. These should therefore, also not be used for non-boolean returning functions or variables.

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
