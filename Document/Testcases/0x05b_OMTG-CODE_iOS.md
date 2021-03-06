## <a name="OMTG-CODE-001"></a>OMTG-CODE-001: Testing for Debug Build

### White-box Testing

1. Import the source code into the xCode Editor.
1. Check the project's build settings for 'DEBUG' parameter under "Apple LVM – Preprocessing" -> "Preprocessor Macros".
1. Check the source code for NSAsserts method and its companions.

### Black-box Testing

This test case should be performed during White-box testing.

### Remediation

Once you have deployed an iOS application, either through the App Store or as an Ad Hoc or Enterprise build, you won't be able to attach Xcode's debugger to it. To debug problems, you need to analyze Crash Logs and Console output from the device itself. Remove any NSLog calls to prevent debug leakage through the Console.

### References
TUDU

## <a name="OMTG-CODE-002"></a>OMTG-CODE-002: Testing for Exception Handling

### White-box Testing

(Describe how to assess this with access to the source code and build configuration)

### Black-box Testing

[Describe how to test for this issue using static and dynamic analysis techniques. This can include everything from simply monitoring aspects of the app’s behavior to code injection, debugging, instrumentation, etc. ]

### Remediation

[Describe the best practices that developers should follow to prevent this issue]

### References

- [link to relevant how-tos, papers, etc.]


## <a name="OMTG-CODE-003"></a>OMTG-CODE-003: Testing for Secure Compiler Flags

### White-box Testing

#### With otool :

* Check if the stack smashing protection is enabled :

```
$ otool -Iv <app name> | grep stack
```

If the application was compiled with the stack smashing protection two undefined symbols will be present: "___stack_chk_fail" and "___stack_chk_guard".

* Check the PIE protection is enabled :

```
$ otool -Iv <app name> | grep PIE
```

If the above command emit no output then the PIE protection isn't enabled. 

* Check the ACR protection is enabled :

```
$ otool -Iv <app name> | grep _objc_release
```

If the above command emit no output then the ACR protection isn't enabled.

#### With idb :

IDB automates the process of checking for both stack canary and PIE support. Select the target binary in the IDB gui and click the "Analyze Binary…" button.

![alt tag](https://github.com/OWASP/owasp-mstg/blob/master/Document/images/idb.png)


### Black-box Testing

This test case should be performed during White-box testing.

### Remediation

* Stack smashing protection 

Steps for enabling Stack smashing protection within an iOS application :

1. In Xcode, select your target in the "Targets" section, then click the "Build Settings" tab to view its settings.
1. Verify that "–fstack-protector-all" option is selected under "Other C Flags" section.

* PIE support

Steps for building an iOS application as PIE :

1. In Xcode, select your target in the "Targets" section, then click the "Build Settings" tab to view its settings.
1. For iOS apps, set iOS Deployment Target to iOS 4.3 or later. For Mac apps, set OS X Deployment Target to OS X 10.7 or later.
1. Verify that "Generate Position-Dependent Code" is set at its default value of NO.
1. Verify that Don't "Create Position Independent Executables" is set at its default value of NO.

* ARC protection 

Steps for enabling ACR protection within an iOS application :

1. In Xcode, select your target in the "Targets" section, then click the "Build Settings" tab to view its settings.
1. Verify that "Objective-C Automatic Reference Counting" is set at its default value of YES.


### References

* Technical Q&A QA1788 Building a Position Independent Executable : https://developer.apple.com/library/mac/qa/qa1788/_index.html
* idb : https://github.com/dmayer/idb

## <a name="OMTG-CODE-004"></a>OMTG-CODE-004: Testing for Unreacheble/Dead code

### White-box Testing

(Describe how to assess this with access to the source code and build configuration)

### Black-box Testing

[Describe how to test for this issue using static and dynamic analysis techniques. This can include everything from simply monitoring aspects of the app’s behavior to code injection, debugging, instrumentation, etc. ]

### Remediation

[Describe the best practices that developers should follow to prevent this issue]

### References

- [link to relevant how-tos, papers, etc.]
