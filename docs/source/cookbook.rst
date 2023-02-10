X++ Cookbook
============

Creating aggregate table views with tmp tables
----------------------------------------------
The following example is the x++ code requiured to populate a tmp table with a view of workers by BirthYear with counts of various email domains 

.. code-block:: X++

    public class ExampleSummaryTmpTable extends common
    {
        /// <summary>
        /// Populates the table with data from hcmWorker by BirthYear, aggregating counts of email domains
        /// </summary>
        /// <param name="directReportsOnly">
        /// Whether to get the whole reporting structure or just direct reports
        /// </param>
        [Hookable(False)]
        public void populateTable(boolean directReportsOnly = true)
        {
            DirPersonBaseEntity dirPerson;

            // Set up Query for Course fetch
            QueryRun qr = new QueryRun(new Query());
            QueryBuildDataSource qdbsWorker = qr.query().addDataSource(tableNum(HcmWorker));

            QueryBuildDataSource qdbsDirPersonEntity = qdbsWorker.addDataSource(tableNum(DirPersonBaseEntity));

            qdbsDirPersonEntity.joinMode(JoinMode::InnerJoin);
            qdbsDirPersonEntity.addLink(fieldNum(HcmWorker, Person), fieldNum(DirPersonBaseEntity, RecId));
            qdbsDirPersonEntity.addOrderByField(fieldNum(DirPersonBaseEntity, BirthYear));

            // Setup ranges to include only reporting structure
            HcmWorker::rangeFilterReports(HcmWorkerLookup::currentWorker(), qdbsWorker , directReportsOnly);

            while (qr.next())
            {
                // Process each record and add to count in each bucket. 
                dirPerson = qr.get(tableNum(DirPersonBaseEntity));

                if (this.BirthYear != dirPerson.BirthYear)
                {
                    //when finished with a particular birth year, write the aggregate values to the tmp table
                    this.writeCurrentRecord(); 
                }
                this.BirthYear = dirPerson.BirthYear;
                if (strFind(dirPerson.PrimaryContactEmail, "@gmail.com"))
                {
                    this.Completed++;
                }
                else if (strFind(dirPerson.PrimaryContactEmail, "@yahoo.com"))
                {
                    this.Yahoo++;
                }
                else if (strFind(dirPerson.PrimaryContactEmail, "@outlook.com"))
                {
                    this.Outlook++;
                }
                else
                {
                    this.Other++;
                }
                this.Total++;
            }
            // write last record
            this.writeCurrentRecord();
        }

        private void writeCurrentRecord(){
            if(this.BirthYear != "") 
            {
                ttsbegin;
                this.write();
                ttscommit;
            }
            this.clear();
            this.Gmail = 0;
            this.Yahoo = 0;
            this.Outlook = 0;
            this.Other = 0;
        }
    }

In order to populate this temp table all you need to do is add the following code to the init method of the form part you wish to use this table as a datasource to

.. code-block:: X++

    public class MyReportsEmailDomainsReportFormPart extends FormRun
    {
        public void init()
        {
            super();
            ExampleSummaryTmpTable.populateTable(true);
        }

    }