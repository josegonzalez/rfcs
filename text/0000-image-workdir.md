# Meta
[meta]: #meta
- Name: Set Image Working Directory to value of CNB_APP_DIR
- Start Date: 2021-01-13
- Author(s): @josegonzalez
- RFC Pull Request: (leave blank)
- CNB Pull Request: (leave blank)
- CNB Issue: (leave blank)
- Supersedes: N/A

# Summary
[summary]: #summary

This RFC proposes setting the Working Directory property of run images to the value of `CNB_APP_DIR`.

# Definitions
[definitions]: #definitions

N/A

# Motivation
[motivation]: #motivation

This change will enable platforms to more easily introspect on the correct working directory for
exec'ing into a container without being tied to CNBs as the foundation for image building. Without
this change, platforms will need to special-case CNB images to ensure entering new or existing
containers is performed in the correct path.

Additionally, copying files from an image may be incorrect if the value is not introspected properly
for CNB images.

# What it is
[what-it-is]: #what-it-is

The proposes one change

- Injection of `/workspace` - the value of `CNB_APP_DIR` - as the WorkingDir of built images

# How it Works
[how-it-works]: #how-it-works

The Exporter.Export() would need to be modified to call `Image.SetWorkingDIr()` with the correct value.

# Drawbacks
[drawbacks]: #drawbacks

It is less code to do so.

# Alternatives
[alternatives]: #alternatives

N/A

# Prior Art
[prior-art]: #prior-art

N/A

# Unresolved Questions
[unresolved-questions]: #unresolved-questions

N/A

# Spec. Changes (OPTIONAL)
[spec-changes]: #spec-changes

- There would be a new property - `WorkingDir` - on exported images that was previously an empty string and will now contain the value of `CNB_APP_DIR`.
