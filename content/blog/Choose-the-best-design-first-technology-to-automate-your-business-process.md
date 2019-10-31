---
title: "Choose the Best Design First Technology to Automate Your Business Process"
date: 2019-11-01T00:22:11+05:30
draft: false
---

<p>You want to choose a technology to automate the booking process for your bike rental business.</p>
<p>You want to streamline and modernize this process as it is performed on your original campus. You also want to integrate a bike tracking technology that is used on the new campus where you've recently obtained the rights to operate the existing bike rental business.</p>
<p>In this exercise, we'll examine this scenario in detail and choose which technology to use.</p>
<h2 id="scenario">Scenario</h2>
<p>On your original campus, you have five bike rental shops. Each shop has a list of bikes for rent and its own database that records the bikes and their features and whether they are already rented or in the shop.</p>
<p>Currently, each bike can only be rented from its home shop. When a customer returns a bike to another shop, your staff move it back to the shop where it is listed on the database. You'd like to change the process so that each bike can be rented from any shop. However, you want to ensure staff can find out quickly where each bike is.</p>
<p>At the university in the next state, the bike rental business invested in a third party system to track bike locations. When a bike arrives back at a store, a unique barcode on the crossbar is scanned. The bike tracking database is automatically updated with the name of the shop that scanned the barcode. When a bike leaves a shop with a customer, the location is changed to &quot;On Hire&quot; and the customer name is recorded in a separate column.</p>
<p>This system has proved helpful when a customer asks for a bike with specific frame size and/or specific features, such as an electric motor or all-terrain suspension. If a shop doesn't have a bike with the right equipment, the shop can quickly find out where such a bike is and get it or send the customer to the right shop. This bike location database has a REST API that you can call from other systems.</p>
<p>Your managing director wants to be able to understand clearly the workflow that you develop. There were problems in the past when documentation has not been kept in-sync with custom code and your director wants to see the process as it's implemented.</p>
<h2 id="business-process">Business Process</h2>
<p>You want to update the bike reservation and rental process on both campuses to the following workflow:</p>
<p><img src="media/4-bike-hire-workflow.png" alt="Bike booking and rental workflow" data-linktype="relative-path"></p>
<p>The details are as follows:</p>
<ol>
<li>A customer requests a bike on the phone, in person, or through the website.</li>
<li>Shop staff record the customer's details and frame size.</li>
<li>Does the customer need specific features such as an electric motor, suspension, or a child trailer? If so what are those features?</li>
<li>Where are all the bikes with that frame size and  those features? This information is obtained from the bike location database and is kept up-to-date by the barcode scanning system.</li>
<li>Is there a bike with the right features and frame size in the right shop? If yes book that bike.
<ol>
<li>If not, where is the nearest bike? Reserve that bike.</li>
<li>Send an email to staff to move the bike to the customer.</li>
<li>Scan barcode in new location.</li>
</ol>
</li>
<li>Give the bike to the customer and update location to &quot;On Hire&quot;.</li>
<li>Take payment from the customer.</li>
</ol>
<p>This is a simplification of the entire process. For simplicity, we've omitted edge cases such as no bike with the desired frame size or features is available for rent. Perhaps you can think of other cases not covered by this simplified process.</p>
<h2 id="choosing-a-technology">Choosing a technology</h2>
<p>Let's look at the Azure technologies available to implement the business process and integrate with the bike location database:</p>
<ul>
<li>Microsoft Flow</li>
<li>Azure Logic Apps</li>
<li>Azure Functions</li>
<li>Azure Service Apps WebJobs</li>
</ul>
<p>You could use any of these technologies and others to build a workflow for this business process. Each technology can also integrate with any REST API, so you could also use any of these technologies to integrate with the bike location system. How then, can you choose?</p>
<h3 id="design-first-or-code-first">Design-first or code-first?</h3>
<p>We know that your Managing Director and her staff want to understand the workflow and a higher level than examining the code and implementation. She also doesn't like separate documents describing a process, because it so easily becomes out-of-date when the process changes.</p>
<p>If you choose a design-first approach, the workflow is visualized in an easy-to-understand design surface. In addition, that diagram is not a separate document, but a picture of the process as it is implemented. The benefit is that there's no possibility that the diagram is not updated when the process is changed.</p>
<p>For this reason, choose a design-first approach.</p>
<h3 id="microsoft-flow-or-azure-logic-apps">Microsoft Flow or Azure Logic Apps?</h3>
<p>Now you must choose from the two design-first technologies:</p>
<ul>
<li>Microsoft Flow</li>
<li>Azure Logic Apps</li>
</ul>
<p>There's no suggestion in the scenario that shop staff should be able to modify the business process. In addition, to connect to the bike location database through its REST API, you will need to create a custom connector. This is a developer task.</p>
<p>It seems sensible that the development of the custom connector and the workflow should be done by the same person or team. Since these must be developers, it's best to use Azure Logic Apps.</p>
<p>As this exercise shows, we can narrow down the technology to use for a given solution by simply understanding the business process and the audience.</p>

