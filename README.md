Remedy Application Statistics
----------------

Thank you for your interest....

Some things to know:
----------------

- Forms and workflow developed using Remedy version 9.x.
- Forms and workflow should work in previous versions of Remedy.
- These forms and workflow were designed for exclusive use in the Remedy Action Request System developed and maintained by BMC Software.
- The Remedy IT Service Management workflow package is recommended but not required if working with solely custom workflow.
- BMC Smart Reporting application is recommended but not required. However, customs forms and Flashboards will need to be created to display much of the data collected and already presented in BMC Smart Reporting.

Installation:
----------------

- Import the DEF file into your Remedy Development environment
1. Open BMC Remedy Developer Studio application
2. Select File drop-down menu and choose Import
3. Follow the steps in the wizard to import all forms and workflow from the DEF file

- Import the XML file into your BMC Smart Reporting Development environment
1. Login to BMC Smart Reporting using account with admin rights
2. Select Administration drop-down menu and choose Import
3. Upload the XML file and follow the steps in the wizard to import the custom Views, Reports, and Dashboards

Post-Installation Updates:
----------------

Once the import of forms and workflow has been completed, you will need to adjust some workflow based on your environment. This workflow was built using a three Remedy application server environment. If you have more than three servers, some extra work might need to be involved to capture their statistical data as well.

- Update LANL:ADM:Combined Application Statistics form
1. Open form LANL:ADM:Combined Application Statistics form in BMC Remedy Developer Studio
2. Rename field "Check Server 1" to actual server name of your first application server
3. (if 2nd server present) Rename field "Check Server 2" to actual server name of your first application server
4. (if 3nd server present) Rename field "Check Server 3" to actual server name of your first application server

- Update LANL:ADM:Combined Server Statistics form
1. Open form LANL:ADM:Combined Server Statistics form in BMC Remedy Developer Studio
2. Rename field "Check Server 1" to actual server name of your first application server
3. (if 2nd server present) Rename field "Check Server 2" to actual server name of your first application server
4. (if 3nd server present) Rename field "Check Server 3" to actual server name of your first application server

- Update Filter Workflow
1. Update the follow Filters to ensure their Qualification statements properly reflect the changed field values from the previous steps.
2. LANL:ADM:Set Server Statistics Server 1
3. LANL:ADM:Set Server Statistics Server 2
4. LANL:ADM:Set Server Statistics Server 3
5. LANL:ADM:Set Application Statistics Server 1
6. LANL:ADM:Set Application Statistics Server 2
7. LANL:ADM:Set Application Statistics Server 3

- Update LANL:ADM:Set Statistic Status Completed
1. Update Filter LANL:ADM:Set Statistic Status Completed to reflect proper number actual servers in your environment.
2. (1 Server) ($Check Server 1$ != $NULL$)
3. (2 Server) ($Check Server 1$ != $NULL$) AND ($Check Server 2$ != $NULL$)
4. (3 Server) ($Check Server 1$ != $NULL$) AND ($Check Server 2$ != $NULL$) AND ($Check Server 3$ != $NULL$)

- Update LANL:ADM:Set App Stat Status Completed
1. Update Filter LANL:ADM:Set App Stat Status Completed to reflect proper number actual servers in your environment.

- Enable Server Statistics
1. Make sure that Server Statistics is enabled on your AR System Administration Console.
2. Workflow built around a setting of 300 seconds (5 minutes) Cumulative Queue collection.

- Enable Application Statistics
1. Login to your Remedy website using an account with admin rights.
2. Open form Application Statistics Configuration (may need to use Mid-Tier Object List).
3. Create entry for each Deployable Application to capture statistics on. For example:
	Logging Status: Enabled
	Logging Type: Application
	Name: Remedy Incident Management
	Logging Interval (sec): 300

You should now be good to start collecting various statistics about your Remedy application's usage by users. Feedback and suggestions are always welcome.

Expanding Beyond Three Application Servers
----------------

If you are using more than three (3) Remedy application servers, then you will need to adjust more workflow to capture data from any other servers beyond the initial three. I prefer to use separate fields to capture data of each server on the forms LANL:ADM:Combined Application Statistics and LANL:ADM:Combined Server Statistics. However, you could potentially reuse existing fields even though this would make it harder to discern individual collected stats from each server when troubleshooting errors or conflicts.

- Form Updates LANL:ADM:Combined Server Statistics
1. Open the form LANL:ADM:Combined Server Statistics in BMC Remedy Developer Studio
2. Add new checkbox field "Check Server 4" or using actual server name
3. Add new Tab for each additional server in group to be collected
4. Copy fields from tab Server 1 into the new tab
5. Rename new fields accordingly (i.e. API Calls Count1 to API Calls Count4)

- Repeat previous steps on form LANL:ADM:Combined Application Statistics

- Create Filter LANL:ADM:Set Server Statistics Server 4
1. Copy filter LANL:ADM:Set Server Statistics Server 1 to LANL:ADM:Set Server Statistics Server 4
2. Update Qualification to reflect the fourth server name in your server group
3. Update Push If Qualification to use new "Check Server 4" field
4. Update Push To Fields to direct data to newly created fields (i.e. $Create Entry Calls Count4$ = $Create Entry Calls Count$)

- Repeat previous step for LANL:ADM:Set Application Statistics Server 4

- Update LANL:ADM:Set Statistic Status Completed
1. Update Qualification to reflect newly created "Check Server 4" field on form LANL:ADM:Combined Server Statistics

- Update LANL:ADM:Set App Stat Status Completed
1. Update Qualification to reflect newly created "Check Server 4" field on form LANL:ADM:Combined Application Statistics

- Repeat for each additional Remedy Application Server.

Authors
----------------
- Forms and workflow developed by James Van Sickle
- Remedy Action Request System developed by BMC Software Inc., © Copyright 2005-2018
- Remedy IT Service Management Suite developed by BMC Software Inc., © Copyright 2005-2018
- BMC Smart Reporting developed by BMC Software Inc., © Copyright 2017-2018

Release
----------------
© (or copyright) 2019. Triad National Security, LLC. All rights reserved.

This program was produced under U.S. Government contract 89233218CNA000001 for Los Alamos National Laboratory (LANL), which is operated by Triad National Security, LLC for the U.S. Department of Energy/National Nuclear Security Administration. 

All rights in the program are reserved by Triad National Security, LLC, and the U.S. Department of Energy/National Nuclear Security Administration. The Government is granted for itself and others acting on its behalf a nonexclusive, paid-up, irrevocable worldwide license in this material to reproduce, prepare derivative works, distribute copies to the public, perform publicly and display publicly, and to permit others to do so.

Release
----------------
Remedy Application Statistics is released under the BSD 3-Clause License. For more details see the
LICENSE.txt file.

LANL code designation: `C18046`
