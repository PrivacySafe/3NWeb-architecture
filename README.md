# 3NWeb Architectural Notes

 - [Raison d'être](#section-raison)
 - [Design considerations](#section-considerations)
 - Implementations and standards
   - sadf


## <a name="section-raison"></a> Raison d'être
 
> Human dignity and human flourishing are intimately bound up in the ability to shape your environment and make an impact on the world around you, to act, rather than be acted upon.
>
> -- Cory Doctorow

Everything in modern society depends on tech. For instance, in Estonia you can't participate in life without electronic id with signatures, and Israel explicitly gives SIM cards for smartphones to new repatriants. Modern life happens in cyberspace, and [tussle happens there as well](https://groups.csail.mit.edu/ana/Publications/PubPDFs/Tussle2002.pdf)
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
> "Tussle in Cyberspace: Defining Tomorrow's Internet", DOI 10.1145/633025.633059, August 2002

Two full decades have passed in this 21st century. And users had unpleasant experiences, like:
 - You use a nice photo album web application, from some vendor. Vendor decides to stop service, and everyone is left scrambling to save photos locally, so as not to loose one's own content. In comparison, when you have an old pc/mac/linux program, you can still run it in some virtual machine.
 - Vendor's employee observes user's communication, messages, content of files.
 - We start to talk about [digital feudalism](https://www.schneier.com/blog/archives/2012/12/feudal_sec.html).

[RFC 8890](https://www.rfc-editor.org/rfc/rfc8890.txt)
> 3. Why the IETF Should Prioritize End Users
>
> Merely advancing the measurable success of the Internet (e.g., deployment size, bandwidth, latency, number of users) is not an adequate goal; doing so ignores how technology is so often used as a lever to assert power over users, rather than empower them.
>
> Beyond fulfilling the IETF's mission, prioritizing end users can also help to ensure the long-term health of the Internet and the IETF's relevance to it.  Perceptions of capture by vendors or other providers harm both; the IETF's work will (deservedly) lose end users' trust if it prioritizes (or is perceived to prioritize) others' interests over them.
>
> Ultimately, the Internet will succeed or fail based upon the actions of its end users, because they are the driving force behind its growth to date.  Not prioritizing them jeopardizes the network effect that the Internet relies upon to provide so much value.


## <a name="section-considerations"></a> Design considerations

