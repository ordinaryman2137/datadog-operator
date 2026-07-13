
▎ PR: #3251 — Provider documentation
▎ Repo: DataDog/datadog-operator
▎ Author: levan-m (internal — this is your own PR)
▎ Files changed: 10 (350 additions, 46 deletions)
▎ Labels: team/container-platform, team/documentation
▎ Reviewers: none assigned
▎ Status: Draft

Note on repo type: datadog-operator isn't the documentation repo, so most files here (providers.md, configuration.v2alpha1.md, control_plane_monitoring.md, etc.) render on GitHub rather than the docs site. Only configuration_public.md (via public_header/footer.markdown) is single-sourced into the public docs build — so Datadog style is strictly binding there, and lighter-touch elsewhere. All internal relative links resolve; the Google Cloud URL resolves (200). The providers.md GitHub blob link 404s only because the file isn't on main yet — it resolves after merge. This is standard for a new-file absolute link, not a fix.

---
Higher-level feedback

1. "profile" is overloaded — provider is defined as an "environment profile" while DAP already means "profile."
Location: Review body
The definition "A provider is a named environment profile…" reuses a word this project already assigns to DatadogAgentProfiles ("DAPs, also known as profiles"). The collision is sharpest in datadog_agent_profiles.md, where the new "Declaring a provider" section has a provider set on a profile that is itself an environment profile. Consider "environment classification," "environment type," or "environment descriptor" to keep "profile" reserved for DAPs. Not blocking — you deliberated on this framing already — but worth a second look now that both terms sit on the same page.

2. providers.md intro second paragraph is abstract and partly restates the first.
Location: docs/providers.md:11
"What warrants a provider is the set of restrictions an environment imposes, not the label of a platform or mode…" uses the "not X, but Y" oppositional framing (an AI-writing marker) and re-explains the "restrictions warrant a provider" idea already conveyed in paragraph 1's examples. The closing "As environments differentiate, a provider can split into more specific ones" is speculative and doesn't help a reader configure anything. Consider cutting this paragraph to 1-2 sentences, or folding its one concrete idea (modes with constraints may need a provider; unrestricted modes may not) into paragraph 1. Gets the reader to "Provider scope" / "Setting a provider" faster.

---
Line-by-line feedback

Must fix

1. Missing comma after introductory phrase.
Location: docs/control_plane_monitoring.md:5
Current: Since Datadog Operator v1.29.0 it is applied automatically based on the detected [provider](providers.md).
Issue: Comma required after the introductory element "Since Datadog Operator v1.29.0."

▎ Since Datadog Operator v1.29.0, it is applied automatically based on the detected provider.

Suggestions

2. Drop "currently" (evergreen docs / avoid list).
Location: docs/control_plane_monitoring.md:5
Current: This feature supports Red Hat OpenShift and Amazon EKS clusters and is currently in Preview.
Issue: "currently" is on the avoid list; docs should read as evergreen.

▎ This feature supports Red Hat OpenShift and Amazon EKS clusters and is in Preview.

3. Redundant clause in General Setup.
Location: docs/control_plane_monitoring.md:31
Current: so a minimal DatadogAgent spec is sufficient and no additional configuration is required.
Issue: "is sufficient" and "no additional configuration is required" say the same thing.

▎ so a minimal DatadogAgent spec is sufficient.

4. provider italicized inconsistently across the config docs.
Location: docs/configuration_public.md:60 (and hack/generate-docs/public_header.markdown)
Issue: providers.md and configuration.v2alpha1.md italicize *provider* on first mention; the public version doesn't. Pick one for consistency. Since the public file is the docs-site one, italics on first mention matches Datadog style.

▎ A provider is a named environment profile—a managed service, distribution, node OS, or an environment with specific restrictions—that the Operator maps to provider-specific configuration.

5. Spaced em dashes in repo docs (consistency + AI-marker overuse).
Location: docs/providers.md (intro, scope, resolution), hack/generate-docs/header.markdown, docs/control_plane_monitoring.md:34
Issue: These files use spaced em dashes (—); Datadog style is no spaces, and the single-sourced configuration_public.md correctly uses unspaced. Not build-affecting on GitHub, but for consistency consider unspaced throughout. Separately, providers.md's intro leans on em dashes heavily — trimming a couple (see higher-level item 2) also reduces the AI-writing tell.

---
Verdict

Comment — one must-fix (the comma) plus minor suggestions; nothing build-breaking. The set is well-structured, the hub-and-spoke design reads cleanly, links resolve, and explicit negation ("are not auto-detected") is handled well for AI readability. The higher-level "profile" overload is the only item I'd genuinely think twice about before publishing. Note the PR is still a draft — worth filling in the PR description (currently the template boilerplate) and assigning the docs team before marking ready.

Would you like me to post this review on the PR? I can:
1. Draft as a pending review (recommended) — walk each comment one at a time, create a pending review; you submit on github.com.
2. Post as a review — same wizard, submitted immediately (would be COMMENT).
3. Post a summary comment — single comment with the full review text.
4. Skip — leave it for you to post manually.





▎ 1. "profile" is overloaded. A provider is defined as an "environment profile," but this project already uses "profile" for DatadogAgentProfiles (DAPs). The collision is sharpest in datadog_agent_profiles.md, where a provider is set on a profile that is itself an environment profile. Consider "environment classification/type/descriptor" to keep "profile" reserved for DAPs.
▎
▎ 2. providers.md intro (2nd paragraph). "What warrants a provider is the set of restrictions… not the label of a platform or mode" uses oppositional "not X, but Y" framing (an AI-writing tell) and largely restates paragraph 1; the closing "a provider can split into more specific ones" is speculative. Consider trimming to 1-2 sentences so readers reach "Setting a provider" faster.
▎
▎ 3. Em dash spacing (minor). providers.md, header.markdown, and control_plane_monitoring.md use spaced em dashes; Datadog style is unspaced, and the single-sourced configuration_public.md already uses unspaced. Consider aligning for consistency.
▎