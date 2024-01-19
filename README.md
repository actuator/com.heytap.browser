## Vulnerability Report

### Overview:
A Remote Code Execution (RCE) vulnerability has been discovered in the `com.heytap.browser` application on the Android platform. The vulnerability allows an attacker to execute arbitrary JavsScript code within the context of the application without any permissions.

### Application Details:

- **Vendor:** - ColorOS
- **Application Name:** 'Internet Browser' `com.heytap.browser`
- **Version:** 45.10.3.4.1
- **Component:** com.android.browser.RealBrowserActivity

### Vulnerability Details:

- **Vulnerability Type:** Arbitrary JavaScript Code Execution
- **Attack Vector:** Via an exported activity component
- **Permissions Required:** None

### Description:

The `com.android.browser.RealBrowserActivity` activity in the `com.heytap.browser` app is exported and can be invoked by any third-party application without requiring any permissions. A malicious app can exploit this to execute arbitrary JavaScript code within the context of the `com.heytap.browser`` application.

This vulnerability is particularly concerning because:
- The victim does not need to grant any special permissions to any installed applications.
- The attack can be initiated remotely.

### Proof of Concept (PoC):


```
{
        super.onCreate(savedInstanceState);

        String javaScriptCommand = "javascript:alert%28%27Test%20Alert%27%29%3B";

        Intent intent = new Intent(Intent.ACTION_VIEW);
        intent.setData(Uri.parse(javaScriptCommand));
        intent.setClassName("com.heytap.browser", "com.android.browser.RealBrowserActivity");

        startActivity(intent);

        finish();
    }
```


### Impact:

Successful exploitation allows an attacker to:
- Execute arbitrary JavaScript code within the context of the `com.heytap.browser` app.


### Mitigation and Recommendations:

1. **Restrict Activity Export:** Do not export activities unless necessary.


