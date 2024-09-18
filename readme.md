# Social Media Activity Checker

This Java application checks the social media activity of a company based on its domain. It currently supports Facebook, LinkedIn, and Instagram.

## Features

- **Facebook Activity Check**: Uses the Facebook Graph API to check activity.
- **LinkedIn Activity Check**: Placeholder for LinkedIn activity check.
- **Instagram Activity Check**: Placeholder for Instagram activity check.

## Usage

1. **Update the code**:
    - Replace `example.com` with the domain you want to check.
    - Replace `YOUR_ACCESS_TOKEN` with a valid Facebook Graph API token.

2. **Run the application**:
    ```sh
    javac com/company/SocialMediaChecker.java
    java com.company.SocialMediaChecker
    ```

## Code Overview

```java
package com.company;

import java.io.IOException;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import com.google.gson.JsonObject;
import com.google.gson.JsonParser;

public class SocialMediaChecker {

    private static final HttpClient client = HttpClient.newHttpClient();

    public static void main(String[] args) {
        String companyDomain = "example.com";  // Replace with the domain you want to check
        checkSocialMediaActivity(companyDomain);
    }

    public static void checkSocialMediaActivity(String domain) {
        String[] socialMediaLinks = findSocialMediaLinks(domain);

        for (String link : socialMediaLinks) {
            if (link.contains("facebook.com")) {
                checkFacebookActivity(link);
            } else if (link.contains("linkedin.com")) {
                checkLinkedInActivity(link);
            } else if (link.contains("instagram.com")) {
                checkInstagramActivity(link);
            } else {
                System.out.println("Unknown social media platform: " + link);
            }
        }
    }

    public static String[] findSocialMediaLinks(String domain) {
        return new String[]{
                "https://www.facebook.com/examplecompany",
                "https://www.linkedin.com/company/examplecompany",
                "https://www.instagram.com/examplecompany"
        };
    }

    public static void checkFacebookActivity(String facebookUrl) {
        System.out.println("Checking Facebook activity for: " + facebookUrl);

        String apiUrl = "https://graph.facebook.com/v12.0/"; // Facebook Graph API URL

        HttpRequest request = HttpRequest.newBuilder()
                .uri(URI.create(apiUrl))
                .header("Authorization", "Bearer YOUR_ACCESS_TOKEN")  // Replace with a real token
                .build();

        try {
            HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
            JsonObject jsonResponse = JsonParser.parseString(response.body()).getAsJsonObject();
            System.out.println("Facebook response: " + jsonResponse.toString());
        } catch (IOException | InterruptedException e) {
            e.printStackTrace();
        }
    }

    public static void checkLinkedInActivity(String linkedInUrl) {
        System.out.println("Checking LinkedIn activity for: " + linkedInUrl);
    }

    public static void checkInstagramActivity(String instagramUrl) {
        System.out.println("Checking Instagram activity for: " + instagramUrl);
    }
}
```

## Dependencies

- [Gson](https://github.com/google/gson): For JSON parsing.
- Java 11 or higher.



## Testing

To run the unit tests, use the following command:

```sh
mvn test
```

The tests are located in the `src/test/java/com/company` directory and use JUnit 4 for testing.

## Building the Project

To build the project and create a JAR file, use the following command:

```sh
mvn package
```

The resulting JAR file will be located in the `target` directory.

## Running the Application

After building the project, you can run the application using the following command:

```sh
java -cp target/social-media-activity-checker-1.0-SNAPSHOT.jar com.company.SocialMediaChecker
```