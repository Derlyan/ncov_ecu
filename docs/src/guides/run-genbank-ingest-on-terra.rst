*********************************************
Ingest SARS-CoV-2 data from GenBank on Terra
*********************************************

We have provided two pipelines for importing data into Terra:

* **GenBank Ingest - pull a public dataset and send them through our preprocessing scripts.**
* GISAID Ingest - pull a private dataset if a user has their own API endpoint, username, and password.

The pipelines were mainly motivated to provide access to our data pre-processing scripts. Currently, these are focused on pulling datasets for the ncov workflow and is roughly diagrammed below:

.. image:: ../images/terra-ingest.png

This guide describes the **GenBank Ingest**.

Import the GenBank ingest wdl workflow from Dockstore
======================================================

1. `Set up a Terra account <https://terra.bio/>`_.
2. Navigate to one of the following in Dockstore:
    - `nextstrain/ncov/genbank_ingest`_: for open (GenBank) data
3. At the top right corner, under **Launch with**, click on **Terra**. You may be prompted to log in.
4. Provide a **Workflow Name** (e.g. ``genbank_ingest`` ).
5. Select a **Destination Workspace** from the dropdown menu.
6. Click **IMPORT**.
7. In your workspace, click on the **WORKFLOWS** tab and verify that the imported workflow is showing a card.

.. _`nextstrain/ncov/genbank_ingest`: https://dockstore.org/workflows/github.com/nextstrain/ncov/genbank_ingest:master?tab=info

Connect any workspace variables to the wdl ingest workflow
===========================================================
  
1. Navigate back to the **Workflow** tab, and click on the workflow imported to your workspace.
2. Click on the radio button **Run workflow(s) with inputs defined by data table**.
3. Under **Step 1**:

  1. Select root entity type as **ncov_examples** from the drop down menu.

4. Under **Step 2**:

  1. Click **SELECT DATA**.
  2. Select **Choose specific ncov_examples to process**.
  3. Select the 1st row in the data table. The first column should have value ``blank``. Selecting more rows will cause the workflow to run more than once.
  4. Click **OK**.

5. Leave the values blank.
6. Click on the **OUTPUTS** tab.
7. Connect your generated output back to the workspace data, but filling in values:

  +-----------------+------------------+-------+----------------------------------+
  |Task name        | Variable	       | Type  |   Attribute                      |
  +=================+==================+=======+==================================+
  |Nextstrain_WRKFLW|  metadata_tsv    | File  | workspace.genbank_metadata_tsv   |
  +-----------------+------------------+-------+----------------------------------+
  |Nextstrain_WRKFLW|  nextclade_tsv   | File  | workspace.genbank_nextclade_tsv  |
  +-----------------+------------------+-------+----------------------------------+
  |Nextstrain_WRKFLW|  sequences_fasta | File  | workspace.genbank_sequences_fasta|
  +-----------------+------------------+-------+----------------------------------+


8. Click **SAVE** then **RUN ANALYSIS**.
9. Optionally enter a job description, then click **LAUNCH**.
10. The new job will appear in the **JOB HISTORY** tab. You can monitor its status by refreshing that page.
11. When run is complete, check the **DATA** / **Workspace Data** tab and use the "workspace.genbank_sequences_fasta" and "workspace.genbank_metadata.tsv" during normal ncov Terra runs.

