#
# Conditional chooser
#

#
# Set File_xxx_Default
#
if(NOT File_SourceFile_Default)
    message(STATUS "Setting File_xxx_Default")
    set(File_SourceFile_Default "src/main.c" CACHE INTERNAL "")
    set(File_DestFile_Default "src/dest.c" CACHE INTERNAL "")
endif(NOT File_SourceFile_Default)

#
# Conditionally decide if file chooser is on or off
# We could use ARCH_IS_X86 directly but assume its
# more complicated.
#
if (ARCH_IS_X86)
    set(USE_FILE_CHOOSER ON)
else()
    set(USE_FILE_CHOOSER OFF)
endif (ARCH_IS_X86)

#
# File chooser
#
if(USE_FILE_CHOOSER)
    # Set the defaults and show
    set(File_SourceFile "${File_SourceFile_Default}" CACHE FILEPATH
	"Select the source file")

    message(STATUS "SourceFile='${File_SourceFile}'")

    set(File_DestFile "${File_DestFile_Default}" CACHE FILEPATH
	"Select the destination file")

    message(STATUS "DestFile='${File_DestFile}'")
else()
    # Unset them so the are removed
    set(File_SourceFile_Default ${File_SourceFile} CACHE INTERNAL "")
    unset(File_SourceFile CACHE)
    set(File_DestFile_Default ${File_DestFile} CACHE INTERNAL "")
    unset(File_DestFile CACHE)
endif(USE_FILE_CHOOSER)

