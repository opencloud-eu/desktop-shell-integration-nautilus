cmake_minimum_required(VERSION 3.16)

# we need at least one language for GNUInstallDirs
project(desktop-shell-integration-nautilus VERSION 1.0.0 LANGUAGES C)

option(REQUIRE_OPENCLOUD_RESOURCES "We depend on the OpenCloud resources, if your distribution does provide alternative icons you can disable this requirement" ON)

include(FeatureSummary)
include(GNUInstallDirs)

if (REQUIRE_OPENCLOUD_RESOURCES)
    find_package(OpenCloudShellResources 1.0.0 REQUIRED)
    set_package_properties(OpenCloudShellResources PROPERTIES TYPE REQUIRED DESCRIPTION "Required OpenCloud resources and icons" URL "https://github.com/opencloud-eu/desktop-shell-integration-resources")
endif()

add_subdirectory(src)

feature_summary(WHAT ALL FATAL_ON_MISSING_REQUIRED_PACKAGES)
