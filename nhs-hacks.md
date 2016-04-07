---
layout: default
title: My NHS Hacks
id: nhs-hacks
active: active
permalink: /nhs-hacks
---

## UK DIGITAL HEALTH CALENDAR
An (inexhaustive) list of major digital health events across the UK – to aid planning of same events. No responsibility is accepted for the accuracy of information contained herein, you are invited to check the dates and venues. Please email marcusbaw@gmail.com with any updates/suggestions. Code to embed this calendar, and links to add it to your own personal calendar are at the bottom of the page.

## BNF SEARCH BAR PLUGIN
Once installed, you can enter search terms straight into the search box in your browser and you will be taken straight to the results of your search, cutting out the BNF front page and saving (a little) time.

INSTALLATION (easy): This page has a html tag in it which alerts your browser to the availability of a search plugin and points it to the URL of the plugin so it can be automatically installed. Simply go to the browser’s Search box, activate the pull down menu and look for: ‘Add “BNF Search”‘. Click this option, and the BNF search will be added to the list of available searches.

Ideally, this plugin would be hosted on the BNF website. If anyone knows the BNF.org admins, can you let them know it is here and they’re welcome to use it.

```
<?xml version=”1.0″ encoding=”UTF-8″?>
<OpenSearchDescription xmlns=”http://a9.com/-/spec/opensearch/1.1/” xmlns:moz=”http://www.mozilla.org/2006/browser/search/”>
<ShortName>BNF</ShortName>
<Description>British National Formulary Search</Description>
<Contact>info@bawmedical.co.uk</Contact>
<InputEncoding>UTF-8</InputEncoding>
<Image width=”16″ height=”16″ type=”image/x-icon”>http://www.bnf.org/bnf/favicon.ico</Image>
<Url type=”application/x-suggestions+json” method=”GET”
template=”http://www.bnf.org/bnf/search.htm?q={searchTerms}” />
<Url type=”text/html” method=”GET” template=”http://www.bnf.org/bnf/search.htm?”>
<Param name=”q” value=”{searchTerms}*”/>
</Url>
<SearchForm>http://www.bnf.org/bnf/index.htm</SearchForm>
</OpenSearchDescription>
```

## AUTOHOTKEY
AutoHotKey is a free, open source programming language for Windows that is very easy to get started with and learn basic features, although it has rich functionality. It is mainly used for automation of simple tasks in Windows, to save time when typing and speed up repetitive tasks. Unfortunately, as a result of my recent switch to Linux (Xubuntu) as my main operating system, I have not really been actively developing these tools in the last few months since November 2012. There is a cross-platform compatible implementation of the AutoHotKey language being developed for Linux (IronAHK), however it’s currently early in development and not really ready for use.

[Please note that most of these scripts I have not written myself. In most cases they were cut & pasted from published open code on the AHK Forums, which are very useful. I have, where possible, tried to maintain attribution of the work to the correct author, please accept my apologies if I’ve missed anyone off, and of course contact me and I will correct it]

When I get time, I will build compiled versions of the scripts too, & link to them, for those who would like to be able to use the script but don’t want to get their hands covered in code!

Caps Lock Tools – disables Caps Lock to avoid “cAPS lOCK fAIL”, which is something I am a bit prone to. Very annoying when you are behind time already, patients are waiting, and you have written 3 or 4 lines’ worth of consultation like this in SystmOne or whatever. I just fire up CLT and can convert the whole lot into sentence case or lower case in one click. (see page)

Numeric Evaluator – evaluates numeric expressions in-situ. (see page)

Auto-expand Abbreviation/Acronym – ‘best practice’ in medical notes is not to use abbreviations/colloquialisms/acronyms unless they are absolutely universal in use (eg “MI” meaning “myocardial infarction” is probably OK, being quite universal, but “no SI/MT” meaning “no suicidal ideation or morbid thoughts” is not widely used) However, it is time consuming to type them all out longhand, so I started collecting together a list of the abbreviations etc I most commonly use, and using AHK to automate expanding them to the full text. When I am in full flow this can save considerable time when documenting a consultation.

‘Medical’ Spellchecker

## CAPS LOCK TOOLS
[Please note that most of these scripts I have not written myself. In most cases they were cut & pasted from published open code on the AHK Forums, which are very useful. I have, where possible, tried to maintain attribution of the work to the correct author, please accept my apologies if I’ve missed anyone off, and of course contact me and I will correct it]

When I get time, I will build compiled versions of the scripts too, & link to them, for those who would like to be able to use the script but don’t want to get their hands covered in code!

GET THE MOST UP TO DATE CapsLockTools HERE:

https://github.com/pacharanero/CapsLockTools

CAPS LOCK TOOLS

Nifty little suite of tools to which disables the Caps Lock key (preventing me typing fOR aGES iN “cAPS lOCK fAIL” – yes I admit I still look mostly down…..) – When the CL key is pressed a menu pops up giving the following options:
The currently selected text is replaced by the same text with the case changed according to the option you select.

Thanks to the contributors to this thread at the AHK forum, from whom I got most of the code. I did make some small edits, essentially amalgamating two versions of the script and a few additions.

## NUMERIC EVALUATOR HOTKEY

Script to evaluate a selected numeric expression in place, replacing the expression with the numeric result of the evaluation. Useful for doing a little bit of in-place maths rather than having to open a calculator. Works anywhere, eg in word processor, text editor, command line etc. Most basic operators * + / – work.

Example: type in “254/7”, select it with mouse, hold Windows key + tap ‘e’ key. Selection is replaced with “36.285714”. The first line “#e::” sets up which key launches the script, this can be changed to anything you like. Consult the AHK docs for further info on how. Thanks to Laszlo on the AHK forums for this one:

```
;-----------------------------------------------------------------------------------------------------------
;EVALUATE THE SELECTION ARITHMETICALLY (simple arithmetic in selection will be evaluated & will replace selection)
;-----------------------------------------------------------------------------------------------------------
#e:: ; Evaluates dynamic expression, replace with
Send ^c
FileDelete $temp$.ahk ; Here will be the temp script written
FileAppend #NoTrayIcon`nClipBoard:=%ClipBoard%, $temp$.ahk
RunWait $temp$.ahk ; Run AHK to execute temp script
Send ^v ; Replace the expression with its result
Return
```
(Please note that most of these scripts I have not written myself. In most cases they were cut & pasted from published open code on the AHK Forums, which are very useful. I have, where possible, tried to maintain attribution of the work to the correct author, please accept my apologies if I’ve missed anyone off, and of course contact me and I will correct it)

## MEDICAL “AUTOCORRECT”
This is an AutoHotKey script that implements MedicalAutoCorrect against common medical mis-spellings. It also auto-expands abbreviations and acronyms. It works with any Windows based GP clinical system, eg Systm1 (tested), EMIS LV (tested), Vision 3 (tested). Also works with standard applications eg Word, Notepad etc. It is based on the AHK script ‘AutoCorrect’, I have just added some ‘medical’ terminology.

I have removed the rest of the ‘AutoCorrect’ word replacements, if you require these it is a simple matter to run that script simultaneously. MedicalAutoCorrect is heavily slanted towards UK General Practice, and, specifically, mine. NO WARRANTY IS MADE ABOUT ITS FITNESS FOR PURPOSE, YOU ARE WHOLLY RESPONSIBLE FOR REVIEWING THE CODE AND DECIDING IF IT IS SAFE TO USE IN YOUR PRACTICE. MYSELF OR OTHER CONTRIBUTORS TO THIS SCRIPT CANNOT BE HELD LIABLE FOR DOCUMENTATION ERRORS AND/OR CLINICAL ERRORS RESULTING FROM ITS USE.

Please feel free to suggest additions or corrections using the comments feature on the bottom of the page.

```
;-----------------------------------------------------------------------------------------------------------
; MEDICAL AUTOCORRECT - NOTES AND DISCLAIMER
;-----------------------------------------------------------------------------------------------------------
; * This is an AutoHotKey script that implements MedicalAutoCorrect against common medical mis-spellings
; * It also auto-expands abbreviations and acronyms.
; * It works with any Windows based GP clinical system, eg Systm1 (tested)
; * Also works with standard applications eg Word, Notepad etc
; * It is based on the AHK script 'AutoCorrect', I have just added some 'medical' terminology.
; I have removed the rest of the 'AutoCorrect' word replacements, if you require these it is a
; simple matter to run that script simultaneously
; * MedicalAutoCorrect is heavily slanted towards UK General Practice, and, specifically, mine.
; * NO WARRANTY IS MADE ABOUT ITS FITNESS FOR PURPOSE, YOU ARE WHOLLY RESPONSIBLE FOR REVIEWING THE CODE
; AND DECIDING IF IT IS SAFE TO USE IN YOUR PRACTICE. CONTRIBUTORS TO THIS SCRIPT CANNOT BE HELD LIABLE
; FOR DOCUMENTATION ERRORS AND/OR CLINICAL ERRORS RESULTING FROM ITS USE.
;-----------------------------------------------------------------------------------------------------------
; MEDICAL AUTOCORRECT - MIS-SPELLINGS
;-----------------------------------------------------------------------------------------------------------
::symtpoms::symptoms
::sytmpoms::symptoms
::ischeamic::ischaemic
::O?E::O/E:
::O.E::O/E:
::O>E::O/E:
::A?C::A/C:
::A7E::A&E
::baldder::bladder
::hypertenion::hypertension
::hernis::hernia
::shoudler::shoulder
::opthalmology::ophthalmology
::nitgh::night
::nigth::night
:C1:dr::Dr.
:C1:DR::Dr.
::migarine::migraine
::asymtpomatic::asymptomatic
:C1:PLNA::PLAN:
;-----------------------------------------------------------------------------------------------------------
; MEDICAL AUTOCORRECT - AUTO-CAPITALISATION
;-----------------------------------------------------------------------------------------------------------
:C1:perla::PERLA
:C1:bp::BP
:C1:med3::MED3
:C1:nad::NAD
;-----------------------------------------------------------------------------------------------------------
; MEDICAL AUTOCORRECT - AUTO-EXPAND ACRONYM
; note - ":C1:" syntax stops AHK from making the replacement text the same case as the hotstring
;-----------------------------------------------------------------------------------------------------------
:C1:SNT::soft & non-tender
:C1:AHT::anti-hypertensive
:C1:AHM::anti-histamine
:C1:CCF::congestive cardiac failure
:C1:AE::air entry
:C1:NCS::nerve conduction studies
:C1:SI/MT::suicidal ideation/morbid thoughts
:C1:URTI::Upper Respiratory Tract Infection
:C1:LRTI::Lower Respiratory Tract Infection
:C1:TMJ::Temporo-mandibular Joint
:C1:UPSI::unprotected sexual intercourse
:C1:OTC::over-the-counter
:C1:AO::ankle oedema
:C1:RIF::right iliac fossa
:C1:LIF::left iliac fossa
:C1:NBT::no bony tenderness
:C1:MCL::medial collateral ligament
:C1:LCL::lateral collateral ligament
:C1:ACL::anterior cruciate ligament
:C1:PCL::posterior cruciate ligament
:C1:NKDA::no known drug allergies
:C1:COCP::combined oral contraceptive pill
:C1:CI::contraindication
:C1:AE::air entry
:C1:CIBH::change in bowel habit
:C1:LLT::lipid lowering therapy
:C1:PN::practice nurse
:C1:HV::health visitor
:C1:MVC::motor vehicle collision
:C1:RTA::road traffic accident
:C1:MTX::methotrexate
:C1:BFZ::bendroflumethiazide
:C1:ABx::antibiotics
:C1:VV::varicose vein
:C1:H/H::hiatus hernia
:C1:NBR::non-blanching rash
:C1:MOI::mode of action
:C1:POV::point of view
:C1:TATT::tired all the time
:C1:ANTT::aseptic non-touch technique
:C1:VA::visual acuity
:C1:HTN::hypertension
:C1:SE::side effect
;-----------------------------------------------------------------------------------------------------------
; MEDICAL AUTOCORRECT - AUTO-EXPAND ABBREVIATION
;-----------------------------------------------------------------------------------------------------------
:C1:2ndry::secondary
:C1:A/C::anticoagulant
:C1:pt::patient
:C1:BrCa::breast cancer
:C1:2ndry::secondary
:C1:MCr::Manchester
:C1:distbn::distribution
:C1:sph::sphincter
:C1:distb::disturbance
:C1:adv::advised
:C1:palpn::palpation
;:C1:LoW::loss of weight commented out as it clashed with the common word "low"
:C1:OtExt::otitis externa
:C1:tfr::therefore
:C1:mfr::manufacturer
:C1:sph distb::sphincter disturbance
:C1:cipro::ciprofloxacin
:C1:erythro::erythromycin
:C1:pen V::penicillin V
:C1:amox::amoxicillin
:C1:trimeth::trimethoprim
:C1:clarith::clarithromycin
:C1:cital::citalopram
:C1:amt::amount
:C1:mirtaz::mirtazapine
:C1:Ix'd::investgated
:C1:Rx'd::prescribed
:C1:infxn::infection
:C1:PUing::passing urine
;-----------------------------------------------------------------------------------------------------------
; ***suffix-O-Fix***
;-----------------------------------------------------------------------------------------------------------
:?:itits::itis
```
