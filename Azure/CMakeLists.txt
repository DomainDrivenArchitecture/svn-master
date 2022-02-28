cmake_minimum_required(VERSION 3.10)

project(test-package VERSION 0.0.2
                    DESCRIPTION "Testing Universal Packages on Azure Devops")

set(WD ${CMAKE_SOURCE_DIR}/TestPackage)

add_custom_target(publish
    WORKING_DIRECTORY
        ${WD}
    COMMENT
        "Publishes Folder 'TestPackage' to Azure"
    COMMAND
        az artifacts universal publish
            --organization https://dev.azure.com/assysteme/
            --project="Weinig"
            --scope project
            --feed test-feed
            --name ${PROJECT_NAME}
            --version ${PROJECT_VERSION}
            --description "Testing Universal Packages"
            --path .)

set(EXECUTABLE_OUTPUT_PATH ${CMAKE_SOURCE_DIR}/bin)
add_executable(main ${WD}/main.cpp)
target_compile_features(main PRIVATE cxx_std_17)