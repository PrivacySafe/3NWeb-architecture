# 3NWeb Architectural Notes

3NWeb is an uncompromisingly user-centric digital space.
Definition of such space has to consist of a bunch of protocols, formats and conventions for writing bodies of software that allow user
 - to operate in a connected cyberspace
 - using one or more devices
 - having a full control over one's tools
 - having a choice of vendors/contractors for underlying tech operations.

3NWeb-following software parts compose together into a coherent operating system for user's stuff in today's digitalized society, ensuring end user's technological sovereignty.

Let's motive focus area and layout details:
 - [Users first](#section-raison)
 - [Wishes](#section-wishes)
 - [Design considerations](#section-considerations)
 - Implementations and standards
   - Basic needs: identity, communication and storage
   - Server-client protocols
   - Stack


## <a name="section-raison"></a> Users first

Everything in modern society depends on tech. For instance, in Estonia you can't participate in life without electronic id with signatures, and Israel explicitly gives smartphone SIM-cards to newly repatriated. Modern life happens in cyberspace making it an important domain of our environment.
 
> Human dignity and human flourishing are intimately bound up in the ability to shape your environment and make an impact on the world around you, to act, rather than be acted upon.
>
> -- Cory Doctorow

At the start of this century tensions have already been noted in the digital domain:
> 2. PRINCIPLES
>
> The thesis of this paper is that the future of the Internet will increasingly be defined
by tussles that arise among the various parties with divergent interests, and that
the technical architecture of the Internet must respond to this observation. If this is
so, are there principles to guide designers, and mechanisms that we should use in
recognition of this fact?
>
> 6. CONCLUSION
>
> ... We, as technical designers, should not try to deny the reality of the tussle, but instead recognize our power to shape it. Once we do so, we acquire a new set of hard, technical problems to solve, and this is a challenge we should step up to willingly.
>
> -- from ["Tussle in Cyberspace: Defining Tomorrow's Internet", DOI 10.1145/633025.633059, August 2002](https://groups.csail.mit.edu/ana/Publications/PubPDFs/Tussle2002.pdf)

Over the next two decades we've seen a rise of monopolists and even talking about [digital feudalism](https://www.schneier.com/blog/archives/2012/12/feudal_sec.html). 2020 saw the following:
> 3. Why the IETF Should Prioritize End Users
>
> Merely advancing the measurable success of the Internet (e.g., deployment size, bandwidth, latency, number of users) is not an adequate goal; doing so ignores how technology is so often used as a lever to assert power over users, rather than empower them.
>
> Beyond fulfilling the IETF's mission, prioritizing end users can also help to ensure the long-term health of the Internet and the IETF's relevance to it.  Perceptions of capture by vendors or other providers harm both; the IETF's work will (deservedly) lose end users' trust if it prioritizes (or is perceived to prioritize) others' interests over them.
>
> Ultimately, the Internet will succeed or fail based upon the actions of its end users, because they are the driving force behind its growth to date.  Not prioritizing them jeopardizes the network effect that the Internet relies upon to provide so much value.
>
> -- from [RFC 8890, August 2020](https://www.rfc-editor.org/rfc/rfc8890.txt)

With this direction of discourse it is not outrages to suggest that we don't have yet a comprehensive solution for user private affairs, completely under average user control. However, we do have working application like PGP, SpiderOak, Signal: all good examples of designs that place user in control of their stuff. 3NWeb effort simply combines working designs into a coherent set on top of which new different applications can be written by developers without a chance to screw user's security, privacy or independence.


## <a name="section-wishes"></a> Wishes

Let's enumerate wishes that may direct and constraint following designs.

In a usual human interaction, if a person is not giving out own information, it doesn't spread by itself. To map usual expectations to digital domain, we want to ensure tight information control. Thankfully, encryption allows to turn plain text content to bulk cipher and a key. Hence, bulk bytes can pass through third parties only in cipher form, with as little metadata as possible.

Human life spans long period, over which artifacts collect, and, for example, a grandfather can show pictures to one's grandchild. We want to have the same timelessness with digital artifacts. On a stand alone computer you can open CorelDraw file, and you may even run some old WordPerfect program on an old operating system inside a virtual machine. We want to have an environment in which users can have applications usable long after original developer company is gone.

It should be easy to write applications, as easy as writing a web page. And no permissions should be needed to participate in the ecosystem. Everything short of permissionless model gets abused by monopolistic tendencies.

User should be able to completely rely on one's own devices, and be able to choose, to mix and match suppliers. Users shouldn't be bound to only single vendor, or only single implementation of major utility functions on which plethora of useful apps runs.

People now have several devices. Applications should be able to run on several user devices at once. Applications should be able to pass messages between different users, as well.


## <a name="section-considerations"></a> Design considerations



