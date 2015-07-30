##############################################################################
#
# The "set_property(CACHE" capability first appeared in CMake version 2.8.0.
# This file will yield a configure-time error with CMake 2.6.4 and earlier...
#
# See also:
#   http://cmake.org/cmake/help/cmake-2-8-docs.html#property:STRINGS
#   http://cmake.org/cmake/help/cmake-2-8-docs.html#command:set
#
cmake_minimum_required(VERSION 2.8.0 FATAL_ERROR)
project(ChoicesChoices)

#
# The "set_property(CACHE" capability first appeared in CMake version 2.8.0.
# This file will yield a configure-time error with CMake 2.6.4 and earlier...
#

#
# Demonstrate using fixed/programmatically-defined/invisible-to-the-user lists
# to fill drop-down combo boxes in cmake-gui (the "values" used for
# the STRINGS property are either simply hard-coded, local, or of CACHE type
# INTERNAL)
#

#
# hard-coded
#
set(BaseName "binary" CACHE STRING
      "BaseName chosen by the user at CMake configure time")

set_property(CACHE BaseName PROPERTY STRINGS binary octal decimal hexadecimal)

message(STATUS "BaseName='${BaseName}'")

#
# local variable
#
set(Language "English" CACHE STRING
"Language chosen by the user at CMake configure time")

set(LanguageValues
"English;Spanish;German;French;Chinese;Japanese;Korean;Hebrew;Arabic;Other")

set_property(CACHE Language PROPERTY STRINGS ${LanguageValues})

message(STATUS "Language='${Language}'")

#
# CACHE INTERNAL
#
set(WrapperLanguage "python" CACHE STRING
 "WrapperLanguage chosen by the user at CMake configure time")

set(WrapperLanguageValues "c#;java;lua;perl;php;python;ruby;tcl" CACHE INTERNAL
 "List of possible values for the Language cache variable")

set_property(CACHE WrapperLanguage PROPERTY STRINGS ${WrapperLanguageValues})

message(STATUS "WrapperLanguage='${WrapperLanguage}'")


#
# Demonstrate using a variable/user-modifiable list to fill a drop-down combo
# box in cmake-gui (the "Values" variable used for the STRINGS property is type
# STRING)
#

set(Color "Red" CACHE STRING
 "Color chosen by the user at CMake configure time")

set(ColorValues "Red;Orange;Yellow;Green;Blue;Violet" CACHE STRING
  "List of possible values for the Color cache variable")

set_property(CACHE Color PROPERTY STRINGS ${ColorValues})

message(STATUS "Color='${Color}'")

#
# Select architecture
#
set(Arch "arm" CACHE STRING
    "Choose processor architecture")

set_property(CACHE Arch PROPERTY STRINGS "x86;arm")

#
# Turn Arch into a BOOL
#
#string(CONCAT V "ARCH_IS_" "${Arch}")
#string(TOUPPER "${V}" V)
#set(${V} BOOL)


#
# Another way to Arch into a BOOL
if ("${Arch}" MATCHES "x86")
    set(ARCH_IS_X86 ON)
elseif ("${Arch}" MATCHES "arm")
    set(ARCH_IS_ARM ON)
else ()
    set(ARCH_IS_UNKNOWN ON)
endif ("${Arch}" MATCHES "x86")


add_subdirectory(src)
