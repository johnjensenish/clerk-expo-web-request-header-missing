# Minimal reproduction of "Invalid request headers" error

## Changes from starter repo

- Newer Clerk package version
- Enabled Metro bundler for the Expo web platform
- Changed sign up flow to use passwordless phone number authentication
- Removed sign in flow & OAuth flow
- Replaced publishable key

## Clerk package version

I'm using `@clerk/clerk-expo` 0.19.4 because that version fixed a bug blocking the Expo web platform. Otherwise, dependencies are unmodified from the starter repository.

## Description

`@clerk/clerk-expo` does not seem to function correctly when running the Expo web platform with the [Metro bundler](https://docs.expo.dev/guides/customizing-metro/#web-support). Our app uses the Metro bundler in order to have one bundler process across platforms.

API calls result in an "Invalid request headers" message.

## Error message

The `signUp.create()` API results in the following error in the Chrome console (formatted for legibility).

```json
[
  {
    "code": "request_header_missing",
    "message": "Invalid request headers",
    "longMessage": "Your Clerk Frontend API is accessible from browsers and native applications. To protect against common web attacks, we require the HTTP Authorization header to be present in native application requests. Make sure the HTTP Authorization header is set a valid Clerk client JWT or set it to an empty string for your first Frontend API request that will return your Clerk client JWT.",
    "meta": {}
  }
]
```

## Reproduction steps

1. `npm install`
2. `npm run web`
3. Enter a valid first name, last name, and phone number.
4. Tap the "Sign Up" button.
5. Actual behavior: Observe the error message in the console log.
6. Actual behavior: The app does not progress.

## Expected behavior

After tapping "Sign Up", the app navigates to the verification code screen.

## Behavior on iOS

The app behaves correctly when using `npm run ios` and an account can be created.
