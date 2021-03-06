enable_testing()

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${PROJECT_SOURCE_DIR}/cmake/")

include_directories(${gtest_SOURCE_DIR}/include ${gtest_SOURCE_DIR})
include_directories("${PROJECT_SOURCE_DIR}/lib")

set(GOOGLIBS ${LIBS} gtest gtest_main)

set(TESTS
  DTMMessageParse
  GBSMessageParse
  GGAMessageParse
  GLLMessageParse
  GSAMessageParse
  GSTMessageParse
  GSVMessageParse
  ParseAltitude
  ParseAngle
  ParseCOGM
  ParseCOGT
  ParseDifferentialCorrectionAge
  ParseDifferentialStationID
  ParseFixStatus
  ParseFloat
  ParseGeoidSeparation
  ParseHDOP
  ParseInteger
  ParseLLL
  ParseLSD
  ParseLatitude
  ParseLongitude
  ParseMSL
  ParseMagneticVariation
  ParseMessageType
  ParseNavMode
  ParsePDOP
  ParseRRR
  ParseResiduals
  ParseSOG
  ParseSV
  ParseSatiliteFixes
  ParseSmode
  ParseSpeed
  ParseStatus
  ParseTalkerID
  ParseTimeStamp_String
  ParseTimeStamp_String_String
  ParseVDOP
  RMCMessageParse
  THSMessageParse
  VTGMessageParse
  ValidateChecksum
  ZDAMessageParse
  )

foreach(Test ${TESTS})
  add_executable(${Test}_Test ${Test}_Test.cpp)
  target_link_libraries(${Test}_Test ${GOOGLIBS} NMEAParser)
  add_test(NAME ${Test} COMMAND ${Test}_Test)
endforeach(Test)
