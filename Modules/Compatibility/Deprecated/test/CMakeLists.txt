itk_module_test()
set(ITKDeprecatedTests
itkAtomicIntTest.cxx
itkConditionVariableTest.cxx
itkSimpleFastMutexLockTest.cxx
)

if (NOT ITK_LEGACY_REMOVE)
  list(APPEND ITKDeprecatedTests itkSpawnThreadTest.cxx)
endif()

CreateTestDriver(ITKDeprecated "${ITKDeprecated-Test_LIBRARIES}" "${ITKDeprecatedTests}")

set(BASELINE "${ITK_DATA_ROOT}/Baseline/Common")
set(TEMP ${ITK_TEST_OUTPUT_DIR})

itk_add_test(NAME itkAtomicIntTest COMMAND ITKDeprecatedTestDriver itkAtomicIntTest)

if(NOT MINGW)
itk_add_test(NAME itkConditionVariableTest COMMAND ITKDeprecatedTestDriver itkConditionVariableTest)
endif()

itk_add_test(NAME itkSimpleFastMutexLockTest COMMAND ITKDeprecatedTestDriver itkSimpleFastMutexLockTest)
# short timeout because failing test will hang and test is quite small
set_tests_properties(itkSimpleFastMutexLockTest PROPERTIES TIMEOUT 60)

if (NOT ITK_LEGACY_REMOVE)
  itk_add_test(NAME itkSpawnThreadTest COMMAND ITKDeprecatedTestDriver itkSpawnThreadTest 100)
endif()
