COMMON_PREPROCESSOR_FLAGS = ['-fobjc-arc', '-mmacosx-version-min=10.7']

COMMON_OTEST_SRCS = [
    'Common/DuplicateTestNameFix.m',
    'Common/NSInvocationInSetFix.m',
    'Common/ParseTestName.m',
    'Common/SenIsSuperclassOfClassPerformanceFix.m',
    'Common/Swizzle.m',
    'Common/TestingFramework.m',
]

COMMON_OTEST_HEADERS = [
    'Common/DuplicateTestNameFix.h',
    'Common/NSInvocationInSetFix.h',
    'Common/ParseTestName.h',
    'Common/SenIsSuperclassOfClassPerformanceFix.h',
    'Common/Swizzle.h',
    'Common/TestingFramework.h',
]

COMMON_REPORTERS_SRCS = [
    'Common/EventGenerator.m',
    'Common/NSFileHandle+Print.m',
    'Common/Reporter.m',
]

COMMON_REPORTERS_HEADERS = [
    'Common/EventGenerator.h',
    'Common/NSFileHandle+Print.h',
    'Common/Reporter.h',
    'Common/ReporterEvents.h',
]

TEXT_REPORTERS_SRCS = COMMON_REPORTERS_SRCS + glob(['reporters/text/**/*.m']) + [
    'reporters/TestResultCounter.m',
]

TEXT_REPORTERS_HEADERS = COMMON_REPORTERS_HEADERS + glob(['reporters/text/**/*.h']) + [
    'reporters/TestResultCounter.h',
]

apple_binary(
    name = 'xctool-bin',
    srcs = glob([
        'Common/**/*.m',
        'xctool/xctool/**/*.m',
        'xctool/xctool/**/*.mm',
    ]),
    headers = glob([
        'Common/**/*.h',
        'xctool/Headers/**/*.h',
        'xctool/xctool/**/*.h',
    ]),
    linker_flags = [
        '-F$DEVELOPER_DIR/Platforms/iPhoneSimulator.platform/Developer/Library/PrivateFrameworks',
        '-F$DEVELOPER_DIR/../SharedFrameworks',
        '-F$DEVELOPER_DIR/Library/PrivateFrameworks',
        '-weak_framework',
        'DVTFoundation',
        '-weak_framework',
        'DVTiPhoneSimulatorRemoteClient',
        '-weak_framework',
        'CoreSimulator',
    ],
    preprocessor_flags = COMMON_PREPROCESSOR_FLAGS + [
        '-DXCODE_VERSION=0630',
    ],
    lang_preprocessor_flags = {
        'CXX': ['-std=c++11', '-stdlib=libc++'],
        'OBJCXX': ['-std=c++11', '-stdlib=libc++'],
    },
    frameworks = [
        '$SDKROOT/System/Library/Frameworks/AppKit.framework',
        '$SDKROOT/System/Library/Frameworks/CoreFoundation.framework',
        '$SDKROOT/System/Library/Frameworks/Foundation.framework',
        '$SDKROOT/System/Library/Frameworks/QuartzCore.framework',
    ],
)

apple_binary(
    name = 'pretty',
    srcs = TEXT_REPORTERS_SRCS,
    headers = TEXT_REPORTERS_HEADERS,
    preprocessor_flags = COMMON_PREPROCESSOR_FLAGS,
    frameworks = [
        '$SDKROOT/System/Library/Frameworks/Foundation.framework',
    ],
)

apple_binary(
    name = 'plain',
    srcs = TEXT_REPORTERS_SRCS,
    headers = TEXT_REPORTERS_HEADERS,
    preprocessor_flags = COMMON_PREPROCESSOR_FLAGS,
    frameworks = [
        '$SDKROOT/System/Library/Frameworks/Foundation.framework',
    ],
)

apple_binary(
    name = 'phabricator',
    srcs = COMMON_REPORTERS_SRCS + glob([
        'reporters/phabricator/**/*.m',
    ]),
    headers = COMMON_REPORTERS_HEADERS + glob([
        'reporters/phabricator/**/*.h'
    ]),
    preprocessor_flags = COMMON_PREPROCESSOR_FLAGS,
    frameworks = [
        '$SDKROOT/System/Library/Frameworks/Foundation.framework',
    ],
)

apple_binary(
    name = 'junit',
    srcs = COMMON_REPORTERS_SRCS + glob([
        'reporters/junit/**/*.m',
    ]),
    headers = COMMON_REPORTERS_HEADERS + glob([
        'reporters/junit/**/*.h'
    ]),
    preprocessor_flags = COMMON_PREPROCESSOR_FLAGS,
    frameworks = [
        '$SDKROOT/System/Library/Frameworks/Foundation.framework',
    ],
)

apple_binary(
    name = 'json-compilation-database',
    srcs = COMMON_REPORTERS_SRCS + glob([
        'reporters/json-compilation-database/**/*.m',
    ]),
    headers = COMMON_REPORTERS_HEADERS + glob([
        'reporters/json-compilation-database/**/*.h'
    ]),
    preprocessor_flags = COMMON_PREPROCESSOR_FLAGS,
    frameworks = [
        '$SDKROOT/System/Library/Frameworks/Foundation.framework',
    ],
)

apple_binary(
    name = 'user-notifications',
    srcs = COMMON_REPORTERS_SRCS + glob([
        'reporters/user-notifications/**/*.m',
    ]),
    headers = COMMON_REPORTERS_HEADERS + glob([
        'reporters/user-notifications/**/*.h'
    ]),
    preprocessor_flags = COMMON_PREPROCESSOR_FLAGS,
    frameworks = [
        '$SDKROOT/System/Library/Frameworks/Foundation.framework',
    ],
)

apple_binary(
    name = 'teamcity',
    srcs = COMMON_REPORTERS_SRCS + glob([
        'reporters/teamcity/**/*.m',
    ]),
    headers = COMMON_REPORTERS_HEADERS + glob([
        'reporters/teamcity/**/*.h'
    ]),
    preprocessor_flags = COMMON_PREPROCESSOR_FLAGS,
    frameworks = [
        '$SDKROOT/System/Library/Frameworks/Foundation.framework',
    ],
)

apple_binary(
    name = 'json-stream',
    srcs = COMMON_REPORTERS_SRCS + glob([
        'reporters/json-stream/**/*.m',
    ]),
    headers = COMMON_REPORTERS_HEADERS,
    preprocessor_flags = COMMON_PREPROCESSOR_FLAGS,
    frameworks = [
        '$SDKROOT/System/Library/Frameworks/Foundation.framework',
    ],
)

apple_binary(
    name = 'otest-query-ios-bin',
    srcs = glob(['otest-query/otest-query-ios/**/*.m']),
    frameworks = [
        '$SDKROOT/System/Library/Frameworks/Foundation.framework',
    ],
)

genrule(
    name = 'otest-query-ios',
    srcs = [
        ':otest-query-ios-bin#iphonesimulator-i386',
        ':otest-query-ios-bin#iphonesimulator-x86_64',
    ],
    out = 'otest-query-ios',
    cmd = 'lipo $SRCS -create -output $OUT',
)

apple_binary(
    name = 'otest-query-osx-bin',
    srcs = COMMON_OTEST_SRCS + glob([
        'otest-query/OtestQuery/**/*.m',
        'otest-query/otest-query-osx/**/*.m',
    ]),
    headers = COMMON_OTEST_HEADERS + glob([
        'otest-query/OtestQuery/**/*.h',
    ]),
    frameworks = [
        '$SDKROOT/System/Library/Frameworks/Foundation.framework',
    ],
)

genrule(
    name = 'otest-query-osx',
    srcs = [
        ':otest-query-osx-bin#macosx-i386',
        ':otest-query-osx-bin#macosx-x86_64',
    ],
    out = 'otest-query-osx',
    cmd = 'lipo $SRCS -create -output $OUT',
)

apple_library(
    name = 'otest-query-lib',
    srcs = COMMON_OTEST_SRCS + glob([
        'otest-query/otest-query-lib/**/*.m',
        'otest-query/OtestQuery/**/*.m',
    ]),
    headers = COMMON_OTEST_HEADERS + glob([
        'otest-query/OtestQuery/**/*.h',
    ]),
    frameworks = [
        '$SDKROOT/System/Library/Frameworks/Foundation.framework',
    ],
)

genrule(
    name = 'otest-query-lib-ios',
    srcs = [
        ':otest-query-lib#iphonesimulator-i386,shared',
        ':otest-query-lib#iphonesimulator-x86_64,shared',
    ],
    out = 'otest-query-lib-ios.dylib',
    cmd = 'lipo $SRCS -create -output $OUT',
)

genrule(
    name = 'otest-query-lib-osx',
    srcs = [
        ':otest-query-lib#macosx-i386,shared',
        ':otest-query-lib#macosx-x86_64,shared',
    ],
    out = 'otest-query-lib-osx.dylib',
    cmd = 'lipo $SRCS -create -output $OUT',
)

apple_library(
    name = 'sim-shim-lib',
    srcs = [
        'Common/Swizzle.m',
        'Common/XcodeRequiredVersion.m',
    ] + glob([
        'sim-shim/sim-shim/**/*.m',
    ]),
    headers = [
        'Common/Swizzle.h',
        'Common/dyld-interposing.h',
        'Common/dyld_priv.h',
    ],
    preprocessor_flags = ['-mmacosx-version-min=10.7'],
    frameworks = [
        '$SDKROOT/System/Library/Frameworks/Cocoa.framework',
    ],
)

genrule(
    name = 'sim-shim',
    srcs = [
        ':sim-shim-lib#macosx-i386,shared',
        ':sim-shim-lib#macosx-x86_64,shared',
    ],
    out = 'sim-shim.dylib',
    cmd = 'lipo $SRCS -create -output $OUT',
)

apple_library(
    name = 'otest-shim',
    srcs = COMMON_OTEST_SRCS + glob([
        'otest-shim/otest-shim/**/*.m',
    ]) + [
        'Common/EventGenerator.m',
    ],
    headers = COMMON_OTEST_HEADERS + glob([
        'otest-shim/otest-shim/**/*.h',
    ]) + [
        'Common/dyld-interposing.h',
        'Common/dyld_priv.h',
        'Common/EventGenerator.h',
        'Common/ReporterEvents.h',
        'Common/XCTest.h',
    ],
    preprocessor_flags = [
        '-DSENTEST_IGNORE_DEPRECATION_WARNING',
        '-F$SDKROOT/Developer/Library/Frameworks',
        '-F$DEVELOPER_DIR/Library/Frameworks',
    ],
    compiler_flags = [
        # otest-shim/otest-shim/otest-shim.m:118:69: warning: trigraph ignored [-Wtrigraphs]
        # [NSRegularExpression regularExpressionWithPattern:@"\\e\\[(\\d;)??(\\d{1,2}[mHfABCDJhI])"
        '-Wno-trigraphs',
    ],
    linker_flags = [
        '-F$SDKROOT/Developer/Library/Frameworks',
        '-F$DEVELOPER_DIR/Library/Frameworks',
    ],
    frameworks = [
        '$SDKROOT/System/Library/Frameworks/Foundation.framework',
        '$PLATFORM_DIR/Developer/Library/Frameworks/XCTest.framework',
        '$SDKROOT/Developer/Library/Frameworks/SenTestingKit.framework',
    ],
)

genrule(
    name = 'otest-shim-ios',
    srcs = [
        ':otest-shim#iphonesimulator-i386,shared',
        ':otest-shim#iphonesimulator-x86_64,shared',
    ],
    out = 'otest-shim-ios.dylib',
    cmd = 'lipo $SRCS -create -output $OUT',
)

genrule(
    name = 'otest-shim-osx',
    srcs = [
        ':otest-shim#macosx-i386,shared',
        ':otest-shim#macosx-x86_64,shared',
    ],
    out = 'otest-shim-osx.dylib',
    cmd = 'lipo $SRCS -create -output $OUT',
)

apple_resource(
    name = 'mobile-installation-helper-resources',
    files = glob(['mobile-installation-helper/*.png']),
    dirs = [],
)

apple_binary(
    name = 'mobile-installation-helper-bin',
    srcs = [
        'mobile-installation-helper/mobile-installation-helper/main.m',
    ],
    frameworks = [
        '$SDKROOT/System/Library/Frameworks/CoreGraphics.framework',
        '$SDKROOT/System/Library/Frameworks/Foundation.framework',
        '$SDKROOT/System/Library/Frameworks/UIKit.framework',
    ],
    deps = [':mobile-installation-helper-resources'],
)

apple_bundle(
    name = 'mobile-installation-helper',
    binary = ':mobile-installation-helper-bin',
    extension = 'app',
    info_plist = 'mobile-installation-helper/mobile-installation-helper/mobile-installation-helper-Info.plist',
)

genrule(
    name = 'xctool-zip',
    deps = [
        ':xctool-bin#macosx-x86_64',
        ':pretty#macosx-x86_64',
        ':plain#macosx-x86_64',
        ':phabricator#macosx-x86_64',
        ':junit#macosx-x86_64',
        ':json-compilation-database#macosx-x86_64',
        ':json-stream#macosx-x86_64',
        ':user-notifications#macosx-x86_64',
        ':teamcity#macosx-x86_64',
        ':mobile-installation-helper#iphonesimulator-i386',
        ':otest-query-ios',
        ':otest-query-osx',
        ':otest-query-lib-ios',
        ':otest-query-lib-osx',
        ':otest-shim-ios',
        ':otest-shim-osx',
        ':sim-shim',
    ],
    srcs = [
        'scripts/create_xctool_zip.sh',
    ],
    cmd = 'scripts/create_xctool_zip.sh ' +
        # Binary
        '-b $(location :xctool-bin#macosx-x86_64) ' +
        # Libs
        '-l $(location :otest-query-lib-ios):' +
           '$(location :otest-query-lib-osx):' +
           '$(location :otest-shim-ios):' +
           '$(location :otest-shim-osx):' +
           '$(location :sim-shim) ' +
        # Libexecs
        '-x $(location :otest-query-ios):' +
           '$(location :otest-query-osx) ' +
        # Mobile installation helper app (only used for the 32-bit simulator)
        '-m $(location :mobile-installation-helper#iphonesimulator-i386) ' +
        # Reporters
        '-r $(location :pretty#macosx-x86_64):' +
           '$(location :plain#macosx-x86_64):' +
           '$(location :phabricator#macosx-x86_64):' +
           '$(location :junit#macosx-x86_64):' +
           '$(location :json-compilation-database#macosx-x86_64):' +
           '$(location :json-stream#macosx-x86_64):' +
           '$(location :user-notifications#macosx-x86_64):' +
           '$(location :teamcity#macosx-x86_64) ' +
        # Output zip location
        '-o $OUT',
    out = 'xctool.zip',
    visibility = ['PUBLIC'],
)

# Minimal xctool which doesn't include mobile-installation-helper.app (only needed for Xcode 5)
# and only includes the json-stream reporter
genrule(
    name = 'xctool-minimal-zip',
    deps = [
        ':xctool-bin#macosx-x86_64',
        ':json-stream#macosx-x86_64',
        ':otest-query-ios',
        ':otest-query-osx',
        ':otest-query-lib-ios',
        ':otest-query-lib-osx',
        ':otest-shim-ios',
        ':otest-shim-osx',
        ':sim-shim',
    ],
    srcs = [
        'scripts/create_xctool_zip.sh',
    ],
    cmd = 'scripts/create_xctool_zip.sh ' +
        # Binary
        '-b $(location :xctool-bin#macosx-x86_64) ' +
        # Libs
        '-l $(location :otest-query-lib-ios):' +
           '$(location :otest-query-lib-osx):' +
           '$(location :otest-shim-ios):' +
           '$(location :otest-shim-osx):' +
           '$(location :sim-shim) ' +
        # Libexecs
        '-x $(location :otest-query-ios):' +
           '$(location :otest-query-osx) ' +
        # Reporters
        '-r $(location :json-stream#macosx-x86_64) ' +
        # Output zip location
        '-o $OUT',
    out = 'xctool-minimal.zip',
    visibility = ['PUBLIC'],
)
