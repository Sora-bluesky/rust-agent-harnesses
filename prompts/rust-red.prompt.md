# Rust Red Prompt

Define the smallest failing Rust behavior before implementing anything.

Instructions:

- name the behavior in one sentence
- identify the exact module, function, or API surface under test
- write the smallest failing test or verification criterion first
- avoid implementation detail assertions unless behavior depends on them
- state which evidence profile will be used later: minimal baseline, workspace baseline, or strict profile
- stop once the failure is precise and reproducible

Output:

- failing test or explicit verification criterion
- short note explaining why this is the smallest useful red step
- selected evidence profile
