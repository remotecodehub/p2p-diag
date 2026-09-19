# Localization

All user-visible text must be resource based.

## Required resources

The resource directory is:

    src/P2PDiag/Resources/Localization/

Required files:

- Strings.resx
- Strings.pt-BR.resx
- Strings.en-US.resx

## Culture responsibilities

Strings.resx provides the neutral/default resource set.

Strings.pt-BR.resx contains Brazilian Portuguese translations.

Strings.en-US.resx contains US English translations.

Project documentation and source comments are written in en-US.

## What must be localized

Localization applies to:

- menus;
- form labels;
- prompts;
- validation;
- help text shown to users;
- errors;
- exceptions shown to users;
- logs;
- progress/status text;
- diagnostic summaries;
- report labels.

Developer-only identifiers, protocol names, enum values used as machine-readable data and source-code identifiers do not need translation.

## Rules

Never concatenate a hard-coded user-facing sentence in presentation code.

Use named resource keys and localized formatting arguments.

Resource keys should be stable and descriptive.

When a diagnostic message includes dynamic data, keep the template in the resource and supply the data as arguments.
