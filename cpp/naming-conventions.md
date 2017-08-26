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
Boolean variable names must not be verbs, but may be past tense verbes. This in order to avoid getters that sound like functions. Names must also not imply another variable type.

```c_cpp
bool m_CallParent; // Not okay. Getter will conflict with function bool callParent()
bool m_ParentCalled; // Okay, but ambigious
bool m_Rectangular; // Okay
bool m_Rectangle; // Not okay, implies a Rectangle type rather than a bool
```

The following verbs: `is`, `must`, `can`, `will`, `has`, and `should`, however, are allowed and recommended only for booleans, and functions that return boolean variables. These should therefore, also not be used for non-boolean returning functions or variables.

```c_cpp
bool m_HasCalledParent; // Okay
bool m_ShouldCallParent; // Okay
bool m_MustCallParent; // Okay
bool m_IsRectangular; // Okay, but strongly prefer m_Rectangular
bool m_IsRectangle; // Okay
```

Functions which merely return a boolean as success result do not apply to this rule.