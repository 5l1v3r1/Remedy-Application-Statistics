Remedy Application Statistics
----------------

Thank you for your interest....

Some things to know:

- These forms and workflow were designed for exclusive use in the Remedy Action Request System developed and maintained by BMC Software.
- The Remedy IT Service Management workflow package is recommended but not required if working with solely custom workflow.
- BMC Smart Reporting application is recommended but not required. However, customs forms and Flashboards will need to be created to display much of the data collected and already presented in BMC Smart Reporting views.
- Forms and workflow developed using Remedy version 9.x.
- Forms and workflow should work in previous versions of Remedy.

Installation:

- Import the DEF file into your Remedy Development environment
- Open BMC Remedy Developer Studio application
- Select File drop-down menu and choose Import
- Follow the steps in the wizard to import all forms and workflow from the DEF file

- Import the XML file into your BMC Smart Reporting Development environment
- Login to BMC Smart Reporting using account with admin rights
- Select Administration drop-down menu and choose Import
- Upload the XML file and follow the steps in the wizard to import the custom Views, Reports, and Dashboards

Post-Installation Updates:

Once the import of forms and workflow has been completed, you will need to adjust some workflow based on your environment. This workflow was built using a three Remedy application server environment. If you have more than three servers, some extra work might need to be involved to capture their statistical data as well.

1. Update LANL:ADM:Combined Application Statistics form
- Open form LANL:ADM:Combined Application Statistics form in BMC Remedy Developer Studio
- Rename field "Check Server 1" to actual server name of your first application server
- (if 2nd server present) Rename field "Check Server 2" to actual server name of your first application server
- (if 3nd server present) Rename field "Check Server 3" to actual server name of your first application server

2. Update LANL:ADM:Combined Server Statistics form
- Open form LANL:ADM:Combined Server Statistics form in BMC Remedy Developer Studio
- Rename field "Check Server 1" to actual server name of your first application server
- (if 2nd server present) Rename field "Check Server 2" to actual server name of your first application server
- (if 3nd server present) Rename field "Check Server 3" to actual server name of your first application server

3. Update Filter Workflow
- Update the follow Filters to ensure their Qualification statements properly reflect the changed field values from the previous steps.
- LANL:ADM:Set Server Statistics Server 1
- LANL:ADM:Set Server Statistics Server 2
- LANL:ADM:Set Server Statistics Server 3
- LANL:ADM:Set Application Statistics Server 1
- LANL:ADM:Set Application Statistics Server 2
- LANL:ADM:Set Application Statistics Server 3

4. Update LANL:ADM:Set Statistic Status Completed
- Update Filter LANL:ADM:Set Statistic Status Completed to reflect proper number actual servers in your environment.
- (1 Server) ($Check Server 1$ != $NULL$)
- (2 Server) ($Check Server 1$ != $NULL$) AND ($Check Server 2$ != $NULL$)
- (3 Server) ($Check Server 1$ != $NULL$) AND ($Check Server 2$ != $NULL$) AND ($Check Server 3$ != $NULL$)

5. Update LANL:ADM:Set App Stat Status Completed
- Update Filter LANL:ADM:Set App Stat Status Completed to reflect proper number actual servers in your environment.

6. Enable Server Statistics
- Make sure that Server Statistics is enabled on your AR System Administration Console.
- Workflow built around a setting of 300 seconds (5 minutes) Cumulative Queue collection.

7. Enable Application Statistics
- Login to your Remedy website using an account with admin rights.
- Open form Application Statistics Configuration (may need to use Mid-Tier Object List).
- Create entry for each Deployable Application to capture statistics on. For example:
	Logging Status: Enabled
	Logging Type: Application
	Name: Remedy Incident Management
	Logging Interval (sec): 300

You should now be good to start collecting various statistics about your Remedy application's usage by users. Feedback and suggestions are always welcome.

Expanding Beyond 3 Application Servers

If you are using more than three (3) Remedy application servers, then you will need to adjust more workflow to capture data from any other servers beyond the initial three. I prefer to use separate fields to capture data of each server on the forms LANL:ADM:Combined Application Statistics and LANL:ADM:Combined Server Statistics. However, you could potentially reuse existing fields even though this would make it harder to discern individual collected stats from each server when troubleshooting errors or conflicts.

1. Form Updates LANL:ADM:Combined Server Statistics
- Open the form LANL:ADM:Combined Server Statistics in BMC Remedy Developer Studio
- Add new checkbox field "Check Server 4" or using actual server name
- Add new Tab for each additional server in group to be collected
- Copy fields from tab Server 1 into the new tab
- Rename new fields accordingly (i.e. API Calls Count1 to API Calls Count4)

2. Repeat previous steps on form LANL:ADM:Combined Application Statistics

3. Create Filter LANL:ADM:Set Server Statistics Server 4
- Copy filter LANL:ADM:Set Server Statistics Server 1 to LANL:ADM:Set Server Statistics Server 4
- Update Qualification to reflect the fourth server name in your server group
- Update Push If Qualification to use new "Check Server 4" field
- Update Push To Fields to direct data to newly created fields (i.e. $Create Entry Calls Count4$ = $Create Entry Calls Count$)

4. Repeat previous step for LANL:ADM:Set Application Statistics Server 4

5. Update LANL:ADM:Set Statistic Status Completed
- Update Qualification to reflect newly created "Check Server 4" field on form LANL:ADM:Combined Server Statistics

6. Update LANL:ADM:Set App Stat Status Completed
- Update Qualification to reflect newly created "Check Server 4" field on form LANL:ADM:Combined Application Statistics

7. Repeat for each additional Remedy Application Server.

Authors
----------------
- Forms and workflow developed by James Van Sickle
- Remedy Action Request System developed by BMC Software
- BMC Smart Reporting developed by BMC Software

Release
----------------
Remedy Application Statistics is released under the BSD 3-Clause License. For more details see the
LICENSE.txt file.

LANL code designation: `C18046`
