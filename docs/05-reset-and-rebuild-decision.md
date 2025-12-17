# Reset and Rebuild Decision

## Overview

During the initial build of my Portable SOC Lab, multiple virtual machines were deployed to establish a Windows Active Directory domain, Linux analyst workstation, and supporting infrastructure. As the environment grew, several interconnected issues emerged, primarily related to DNS resolution, time synchronization, and domain authentication.

While each issue was technically solvable in isolation, their combined impact created compounding complexity that obscured root causes and slowed forward progress.

At this stage, a deliberate decision was made to wipe all virtual machines and rebuild the lab from a clean state.

This document explains why that decision was made, what was learned, and how it informed a stronger rebuild strategy.

---

## What Went Wrong

The initial build encountered repeated challenges in the following areas:

- DNS resolution inconsistencies between Linux and Windows systems
- Improper fallback to public DNS servers during early configuration
- Active Directory dependency order issues
- Domain join failures caused by timing, DNS, and service readiness
- Troubleshooting becoming reactive instead of structured

Although many of these issues were partially resolved, they created a fragile environment where fixes introduced new variables instead of reducing them.

At that point, continued troubleshooting would have resulted in diminishing returns.

---

## Why a Full Reset Was the Right Choice

Resetting the environment was not done due to lack of understanding or effort. It was done intentionally for the following reasons:

- To eliminate hidden misconfigurations introduced during early experimentation
- To enforce correct installation order from the beginning
- To validate that each dependency worked in isolation before moving forward
- To reduce cognitive overhead during troubleshooting
- To document a clean, repeatable build process

In real-world environments, engineers regularly make the decision to rebuild rather than patch endlessly. Knowing when to reset is a critical operational skill.

---

## Lessons Learned

Several key lessons were reinforced during this phase:

- DNS must be correct before Active Directory, not fixed afterward
- Domain controllers should be fully stable before joining clients
- Linux AD integration is highly sensitive to DNS and time sync
- Troubleshooting becomes exponentially harder once multiple systems are misaligned
- Documentation is as important as configuration

These lessons directly informed the rebuild strategy.

---

## Rebuild Strategy and New Order of Operations

The rebuild followed a stricter and more intentional sequence:

1. Proxmox host configuration and networking validation
2. Windows Server installation with static IP and DNS configured first
3. Active Directory Domain Services and DNS deployment
4. Verification of domain resolution and authentication on the domain controller
5. Linux analyst VM installation
6. DNS alignment and time synchronization with the domain controller
7. Active Directory domain join from Linux
8. Validation of domain user authentication on Linux

Each step was validated before moving on to the next.

---

## Outcome

The rebuilt environment successfully achieved:

- Reliable DNS resolution across systems
- Stable Active Directory services
- Linux authentication using domain credentials
- Clean, understandable configuration states
- Confidence in future expansion of the lab

Most importantly, the rebuild produced a clearer mental model of how each component depends on the others.

---

## Closing Notes

This reset represents a normal and healthy part of learning complex systems for the first time.

Progress is not always linear. Sometimes the fastest way forward is to stop, reset, and rebuild with intention.

This repository preserves both the planning artifacts and the lessons learned to reflect how real infrastructure is designed, broken, and improved.
