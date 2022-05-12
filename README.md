TODO: Fill in ...'s, see other templates like https://github.com/iworkforthem/rfc and examples like https://ethereum.org/en/eips/ and https://www.python.org/dev/peps/

# RFC Process

Many changes, including bug fixes, script changes and documentation improvements can be
implemented and reviewed via the normal [GitLab merge request workflow](https://github.com/ghostinthewires/Team-Handbook-Template/tree/master/Team-Handbook-Template/general/contributing).

Some changes though are "substantial", and we ask that these be put
through a bit of a design process and produce a consensus.

The "RFC" (request for comments) process is intended to provide a
consistent and controlled path for new features and changes to enter the infrastructure.

[Active RFC List](https://github.com/Jake-Gillberg/RFCs/pulls)

## When you need to follow this process

You need to follow this process if you intend to make "substantial"
change. What constitutes a
"substantial" change is evolving based on community norms, but may
include the following.

   - ...

Some changes do not require an RFC:

   - Small changes that are covered by the normal [GitLab merge request workflow](https://github.com/ghostinthewires/Team-Handbook-Template/tree/master/Team-Handbook-Template/general/contributing)
   

## What the process is

In short, to get a substantial change made to the infrastructure, one must first get the
RFC merged into the RFC repo as a markdown file. At that point the RFC
is 'active' and may be implemented with the goal of eventual inclusion
into the infrastructure.

* Clone the RFC repo https://github.com/ghostinthewires/Rfcs-Template
* Copy `0000-template.md` to `rfc/0000-my-feature.md` (where
'my-feature' is descriptive. don't assign an RFC number yet).
* Fill in the RFC. Put care into the details: **RFCs that do not
present convincing motivation, demonstrate understanding of the
impact of the design, or are disingenuous about the drawbacks or
alternatives tend to be poorly-received**.
* Submit a merge request (Please name your branch the same as your RFC). As a merge request the RFC will receive design
feedback from the Team, and the author should be prepared
to revise it in response.
* Build consensus and integrate feedback. RFCs that have broad support
are much more likely to make progress than those that don't receive any
comments.
* Eventually, the Team will decide whether the RFC is a candidate
for inclusion into the infrastructure.
* An RFC can be modified based upon feedback from the Team.
* An RFC may be rejected by the Team after discussion has settled
and comments have been made summarizing the rationale for rejection. A member of
the Team should then close the RFC's associated merge request.
* An RFC may be accepted by the Team. A Team
member will merge the RFC's associated merge request, at which point the RFC will
become 'active'.

## The RFC life-cycle

Once an RFC becomes active then authors may begin to plan the change. Becoming 'active' is not a rubber
stamp, and in particular still does not mean the change will ultimately
be made to the infrastructure ; it does mean that the Team has agreed to it in principle
and are amenable to the change.

Furthermore, the fact that a given RFC has been accepted and is
'active' implies nothing about what priority is assigned to its
implementation, nor whether anybody is currently working on it.

Modifications to active RFC's can be done in followup pull requests. We strive
to write each RFC in a manner that it will reflect the final design of
the change; but the nature of the process means that we cannot expect
every merged RFC to actually reflect what the end result will be at
the time of the change; therefore we try to keep each RFC
document somewhat in sync with the change as planned,
tracking such changes via followup merge requests to the document.

## Implementing an RFC

The author of an RFC is not obligated to implement it. Of course, the
RFC author (like any other Engineer) is welcome to post an
implementation for review after the RFC has been accepted.

If you are interested in working on the implementation for an 'active'
RFC, but cannot determine if someone else is already working on it,
feel free to ask (e.g. by leaving a comment on it).

## Reviewing RFC's

...