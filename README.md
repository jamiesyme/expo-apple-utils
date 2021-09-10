# expo/apple-utils

An unstable library for performing Apple API tasks with the unofficial iTunes APIs.

# CHANGES

Oh boy, the hacks...

This repo was cloned from the NPM package that Expo publishes, since they don't publish the public git repo for it.

We needed to patch the code so that asks for MFA tokens from us instead of prompting the command line for them, since we run the program in non-interactive mode.

Specifically, the code that we needed to change was the implementation of `parseAndPromptTFAAsync()`. We replaced the body with `return await _expoHacks_getMfaToken();`, which is a global function that our builder defines.

We didn't need to modify the code that prompts for usernames and passwords, since that actually appeared to be handled by `expo-cli` (which we cloned and patched separately).

Finally, if this ever breaks and you need to modify this, try [de-obfuscating](https://lelinhtinh.github.io/de4js/) the code first to figure out where the changes need to be made. Unfortunately, de-obfuscating produces invalid JS, so we can't save the cleaner code, but it helps hugely as a guide.
