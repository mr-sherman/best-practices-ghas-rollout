# Best Practices for a GitHub Advanced Security Rollout
## A Self-Enablement Approach for Large Organizations

Typically, you don’t want to just turn on advanced security features, we all know the wrath that we will incur from developers if we just turn stuff on and throw results at them.  What we typically had done is this:
 1. We pick a few teams or applications, maybe some that are representative of the rest of the applications that are going to be onboarded.  
 2. Then we remediate the results on those applications
 3. Figure out what worked and what didn’t work in the onboarding of that group of applications, 
 4. Move on to the next group of applications, maybe a larger set using what we learned about onboarding the first group.  
 5. Wash, rinse, repeat, and then you’ve onboarded all the applications, or at least the highest priority ones.

So we have these three activities:  Enable a subset of teams.  Remediate the results.  Measure the results and adjust for the next iteration.

This approach has worked for many companies, and it’s better than an all-at-once enablement, but for large enterprises, what we’ve noticed is that we will eventually get bogged down on the complexities of some repositories, and the rollout slows  Often the representative sample isn’t exactly representative of the whole, and each iteration unveils more and more complexity and challenges.  And since this rollout is being performed somewhat linearly, it seems like progress doesn’t get made and just adds to frustration  

When we encounter problems with scale and time, a good solution is to parallelize processes, and when it comes to onboarding many teams or applications, we can apply that principal.  We can have teams self-enable security features, given a set of tools, procedures, and policies.  In essence, we’re taking the shift left approach of application security and applying it to the rollout of application security.  Instead of a top-down approach executed by organizations who may not be entirely familiar with the subtleties of each application, we can give teams an organization for enablement and support, guidelines for adoption, automated processes for enablement, documentation for deployment and remediation, and clear goals and metrics to achieve. 

When I talk about self-enablement I don’t mean let every team decide who gets to go first.  You can still select teams based on priority.  However, what I do mean is don’t restrict teams from going and doing it for themselves.  Teams that can get going quickly should just do it.  The attention can be given to those teams who are going to need the most help.  We have deployed Advanced Security using this method at large companies, and the results have been positive.  

So let’s revisit our three activities, which we still have to do, but since we’re going to allow for self-enablement we need to wrap these three activities with some prerequisites. 

Prior to teams’ self-enablement, we first need to educate them.  This isn’t just telling them about the product and how to use it, but also about the expectations and goals of the program, how to go about enabling advanced security on their repositories, how to ask for help with the results.  In order to get these teams up to speed, before we educate them, we need good documentation.  All of the procedures should be clearly documented and accessible for teams so they can refer to it while they’re going through their enablement.  But before we document things, we need to decide what to document.  And in order to do that, we need to plan.  Everyone’s favorite thing to do, right?  But it’s the most important.  You can’t achieve any type of self-enablement without planning, without setting up the teams for success.  Planning however can be made easier if you just answer some questions and get some key pieces of information.  

### Planning and Documentation
Planning and Documentation go hand-in-hand.  What you plan, you should write down or formalize in some manner.

This is the information that you’ll need:
An inventory of all your repositories, their programming languages, and their active contributors.  
    - The active contributors number is important for determining license consumption.  
    - The programming languages for each repo is important because we need to see if there are any repos that use languages not supported by CodeQL.  
    - We can also use the programming language info to discover some low-hanging fruit, since codeql is easier to enable on projects that use interpreted languages rather than compiled languages. 

From that list, you need list which of those repositories require the implementation of an appsec program? And of those repos that require an appsec program, which are the ones that are THE most important?

You’ll also need a list of key people:  
 - who owns the appsec program?  
 - Who are the appsec experts or champions if teams have questions during their enablement?  
 - What does the organization look like.  

Other Questions:
 - What types of tools and automation do you have at your disposal to help teams deploy advanced security even faster? 
 - Are there scripts, templates, or images available?  If can get them developed now, it’s even better.  
 - What remediation strategies and policies are going to be employed?   
 - How are you going to prioritize the results?  
 - Are you going to block builds and merges?  
 - How will the backlog be handled?  If a repository has existing vulnerabilities, what’s the strategy for fixing those, with an understanding that changes frequently are being introduced and a developer’s attention is going to be more on those tasks rather than the backlog of vulnerabilities.   
 - What key metrics do want to derive from the alerts?  
 - What needs to be done in order to get the information you need to derive those metrics?  
 - Are there any compliance requirements?  
 - What are you going to do with the information you get?  
 - Can we provide pre-canned reports now?  
 - What are the timelines?  
 - What percentage of teams do you want enabled and when?

### Education and Enablement:
This is where you actually start the practice of selecting teams or allowing some teams to self select.  Using the the repository information that you gathered in the planning phase, and the documentation that you developed, you can inform teams that they’ve been selected to enable advanced security.  You can also ask for some early adopters or volunteers.  The reason why you’re letting a few teams self-select is that you can take advantage of teams that can move quickly and get it enabled and tried out.  Inform them about:  Where to find all of the documentation, where to go and who to ask if they have a question, what are the strategies for remediation, what policies should be in place for a given repo, and what data needs to be made available.  
Once you’ve done the initial onboarding for those teams you’ve selected and teams who are interested, then it’s time to allow them to get going.

Communicate to those teams that they can enable advanced security features in their repositories, providing the documentation.  Those teams can also leverage any automation that was developed.  Create a project board for every team so their progress can be tracked.   Schedule regular open office hours so teams can resolve any issues quickly and provide feedback.  Don’t focus so much on the remediation of vulnerabilities at first.  Let the teams focus on getting scanning working with their processes and getting results out of the tools. 

There may be some edge cases for complex repositories or projects, but this is why we are allowing teams to enable this for themselves.  You need to rely on the expertise that exists on those teams and let them integrate advanced security into their repos in a way that makes sense for that repo.  

Don’t focus so much on the remediation of vulnerabilities at first.  Let the teams focus on getting scanning working with their processes and getting results out of the tools. 

Once code scanning is producing results, then it’s time to focus on remediation.    Again, they can use documentation, office hours or internal expertise to strategize on which vulnerabilities need to get remediated and when.  

You may have to refine the strategy for dealing with existing vulnerabilities, depending on how many were found and what their severity is.    These vulnerabilities or groups of vulnerabilities should be turned into issues or tickets so they can be tracked.  

And as you go through the results of the scans and start fixing problems, you may come up with some strategies or patterns for fixing certain types of vulnerabilities.  This is where you can help refine the documentation by writing qlhelp files.  These ql help files will be displayed in-line when the developer is looking at the results of a scan, so they can benefit from some remediation advice from someone who has already fixed a similar problem. 

For secrets that may have been found - do you want to automatically revoke certain kinds of secrets?  Depending on the volume and the type of secrets found, you may want to automatically revoke them.

### Measurement
You can extract alert data from the repository using the REST API or GraphQL API.  That data can then be imported into a BI tool or a SIEM to derive any metrics that you need to keep track of.  

You can also keep the Sarif results file that comes with every scan, and you can extract the data from the Sarif and import it into any other tool.  However, be mindful that the Sarif contains only the results that were found in that scan.  It doesn’t contain any information about what alerts were resolved or when they were resolved.  

Any reports that you may be interested in retrieving can be automated with GitHub actions, so they can happen on some event or some interval.  

There’s also Security Overview, which is at the organizational level.  It shows the entire organization’s security risk, and you can see how many repos have enabled or have not enabled advanced security.  You can see which repos represent the highest risk, and what kinds of alerts were found.

### Summary
Spend most of the time on planning and documentation.
Realize that once the plan is in place and you enable the teams to implement advanced security, it becomes concurrent and the pace of adoption will accelerate.  However, if you do not plan, give your teams good documentation and enable them through automation, the pace is going to be slowed.  

Allow for self-enablement, even in teams or repositories that have a high priority that you want to go first.  Take advantage of their in-depth knowledge of the repositories.  It’s really good to also ask for volunteers, so that teams who can move quickly and try things out can maybe identify issues early on.

Identify your metrics early and write your reports early so that measurement and  feedback can be executed immediately and you can start seeing value out of the advanced security rollout.

If we really want to involve developers in the appsec process and make them feel like they’re a part of it rather than just having this tool forced on them, then deploying this self-empowered approach to rolling out appsec tools will make them part of the process and make them more appsec aware.  
