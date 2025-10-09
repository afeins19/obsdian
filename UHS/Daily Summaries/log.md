# 10_9_2025 

## what i did today:
- cleaned and processed the final 2 days of september experian collections data so surender could create the monthly repot rollup (pre-service, point of service, post date of services, total pas collections)
- learned about how a dbt project is structured
- looked into incorrectly identified patient access collections "discrepancy" which was actaully correct information
- tried to create my profiles.yml (in ~/.dbt) -> ran into an issues with sql server denying me access when i gave my team service account credentials (even though they worked in the python connection string)
- began thinking of how to model our team's workflow in dbt 
- pulled the daily cash and distributed
- fixed the insurance reseuqencing report (after previous change (i forgot what that was), the slicers broke so i replaced them)
- began working on scheduled auth metrics automation -> noticed the mapping sheet was broken...mapping sheet doesnt have every way that "bonham" was referenced. we should also check other facilities too and add src sys id
