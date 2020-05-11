# iOS-Assets-to-UIImageExtension

It is a program that converts Assets.xcassets file into xcode project for use as UIImage Extension.

It runs in Python.

import os

def to_camel_case(snake_str):
    components = snake_str.split('_')
    return components[0] + ''.join(x.title() for x in components[1:]).replace(" ","")

folderPath = "/Users/jeong/Documents/racos/kiosk/racossystem_kiosk_ios/Kiosk/Assets.xcassets/Image"
folderList = os.listdir(folderPath)

for filename in folderList:
    filteredFileName = filename.split('.')[0]
    camelCasedFileName = to_camel_case(filteredFileName)

    if camelCasedFileName == "":
        continue

    result = "".join([
        '@nonobjc class var {0}: UIImage '.format(camelCasedFileName),
        '{\n',
        '    return UIImage(named: "{0}") ?? UIImage()\n'.format(filteredFileName),
        '}\n'
    ])
    
    print (result)
