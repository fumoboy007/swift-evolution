# Marketing Swift to a Wider Audience

## Introduction

Swift started out as a great new programming language for app development on Apple platforms, but it was [always meant](https://oleb.net/blog/2017/06/chris-lattner-wwdc-swift-panel/#in-which-fields-would-you-like-to-see-swift-in-the-future) to grow beyond that initial use case. Indeed, the community and the Core Team have been pushing Swift into exciting new areas with efforts such as [Swift on Server](https://www.swift.org/documentation/server/), [Embedded Swift](embedded-swift.md), and [Differentiable Programming](https://github.com/apple/swift/blob/main/docs/DifferentiableProgramming.md).

Swift is a general-purpose programming language. Its main design principles—fast, modern, safe—are not specific to a given domain; these are general software engineering principles that any software engineer should be able to appreciate.

## Problem

Although we have [high ambitions](https://github.com/swiftlang/swift-evolution/assets/2100868/21c17356-5403-41f9-a850-050837643586) for Swift adoption outside of the Apple community, the results so far are underwhelming compared to other programming languages.

### Measuring Adoption

It is tricky to measure adoption accurately without access to the download statistics of each programming language. As a proxy, let us look at adoption of Swift for server-side programming since that is currently the most popular area where Swift is used outside of the Apple community.

How do we measure adoption for server-side programming? A rough metric could be the popularity of foundational open-source packages for each programming language. For example, we could look at the popularity of a web services framework like [Vapor](https://github.com/vapor/vapor/) compared to similar packages in other languages. We should choose a package that is unlikely to have overlap with the Apple community—the community we want to exclude from the metric.

Vapor has generally been used to build smaller server-side applications or the frontend of larger server-side applications. [By contrast](https://aws.amazon.com/compare/the-difference-between-grpc-and-rest/), the [gRPC](https://grpc.io) framework has generally been used to build the distributed backend of larger server-side applications. Due to this, it is less likely for gRPC users to have overlap with the Apple community compared to Vapor users, so let us use the popularity of the language-specific gRPC repositories as the metric.

The graph in the following section shows the GitHub star history for the gRPC repository of each programming language. The chosen programming languages are the memory-safe languages [jointly recommended](https://www.nsa.gov/Press-Room/Press-Releases-Statements/Press-Release-View/Article/3608324/us-and-international-partners-issue-recommendations-to-secure-software-products/) by several governments around the world. (Python was excluded because it does not have a language-specific gRPC repository.)

### Interpretation of Adoption Data

![GitHub Star History Graph](marketing-swift-to-a-wider-audience-grpc-github-stars.svg)

The metric is only a rough proxy, so we should only interpret the data at a high level. Even so, one thing is clear: Swift has the flattest trajectory among the 5 languages. The Rust programming language is the most similar to Swift among the 5 languages in that it does not have a garbage collector and became stable relatively recently; however, it has a much steeper trajectory than Swift.

Given that Swift is a fast, modern, and safe programming language that has already proven itself among the Apple community, what are the possible reasons for Swift’s relatively flat trajectory outside of the Apple community?

Certainly, there are more bugs and missing features when using Swift on non-Apple platforms. However, even after foundational improvements like the [concurrency system](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/concurrency/), which was released in 2021, the trajectory of Swift adoption for server-side programming remained almost completely the same. This suggests that there are likely other reasons for Swift’s persistently flat trajectory.

This document details several plausible issues that are holding back Swift adoption outside of the Apple community as well possible changes to address those issues.

## Scope of Document

Unlike most other vision documents, which envision changes to the *language*, this document envisions changes to the *processes* guiding the development of the language.

Similar to other vision documents, this document proposes changes at a high level but each change should still go through the proposal process to gather more comprehensive feedback.

## Proposed Focus Areas

### Avoid Branding Swift as an Apple Product

A large portion of developers outside the Apple community are not enthusiastic about the Apple brand and could have negative bias against Swift due to the strong association with Apple. Therefore, we should avoid branding Swift as an Apple product.

#### Possible Changes

- Move the standard library [documentation](https://developer.apple.com/documentation/swift) from the Apple website to the Swift website.
- Move the Foundation library [documentation](https://developer.apple.com/documentation/foundation) from the Apple website to the `swift-foundation` package’s [Swift Package Index page](https://swiftpackageindex.com/apple/swift-foundation).
- Move the GitHub repositories from the [Apple](https://github.com/apple) organization to a Swift-branded organization.
- Move the [WWDC videos](https://developer.apple.com/videos/swift/) about Swift to a Swift-branded YouTube channel.
- Consider creating an independent legal entity to govern the development of the language.

### All Platforms Are Equal

Similar to the previous section but thinking from a more technical perspective, we should avoid giving preference to Apple platforms. As much as possible, all [supported platforms](https://www.swift.org/platform-support/) should be considered equal. We should even consider de-emphasizing Apple platforms in documentation and discussions to offset the historical bias towards Apple platforms.

#### Possible Changes

- Changes to the language or to foundational packages like `swift-foundation` are not considered complete until they are implemented for all supported platforms.
  - This may already be the motivation for the `swift-foundation` rewrite. However, we should ensure this policy is explicit and enforced.
- Actively encourage feature parity between Xcode and developer tools used by those outside of the Apple community including IDEs, build systems, profilers, etc.
  - One way to do so could be to enforce a policy that requires any new Swift-related features in Xcode to be built on top of generic open-source Swift packages that non-Xcode developer tools can depend on.
- Avoid mentioning Apple platforms first on the Swift website or in documentation.
  - Developers interested in Apple platforms would have already found the Apple website, which has all the relevant information, so there is no need for the Swift website to emphasize Apple platforms.

### No Secrets

A major Big Tech company recently considered replacing C++ with Swift as the default programming language for their huge codebase. A major reason they rejected Swift was the perception that Apple might force disruptive changes without thoroughly and seriously considering community feedback.

#### Possible Changes

- Disallow Apple from announcing platform features that rely on unreviewed language changes.
  - For example, SwiftUI was announced [before](https://forums.swift.org/t/important-evolution-discussion-of-the-new-dsl-feature-behind-swiftui/25168) the result builders feature that it relied on was even proposed. This heavily biased the review process: even if some changes could be made based on community feedback, the proposal effectively could not be rejected.

### Evangelism

Even with the above changes, it takes time to change perceptions. Evangelism can speed up the process.

#### Possible Changes

- Port popular software written in other languages to Swift and directly compare the two implementations using objective metrics.
- Give conference talks focused on the benefits of Swift.
- Talk directly with big companies, industry organizations, and governments about the benefits of Swift.

## Appreciation for Apple

Apple funds most of the development of Swift, so we should consider the return on their investment. The proposed changes would lessen Apple’s control over Swift but the benefits to Apple could be drastic.

A large portion of software that Apple depends on is written by developers outside of the Apple community: [low-level OS software](https://github.com/apple-oss-distributions) and server-side software. Imagine the benefits to security, reliability, and efficiency as that software is migrated to Swift.
