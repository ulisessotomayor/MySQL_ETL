# MySQL_ETL
Long form to wide forms ETL:

CREATE VIEW Googleanalytics2_view AS   
SELECT   
(CAST(bt.date as date)) as Date,   
bt.deviceCategory as Device_Category,    
bt.mobileDeviceInfo as Mobile_Device_Info,
bt.browser as Broswer,
bt.landingPagePath as Landing_Page_Path,
bt.channelGrouping as Channel_Grouping, 
bt.source as Source,
(SUM(case when field = 'medium' then value else null end)) as Medium,
(SUM(case when field = 'adContent' then value else null end )) as Ad_Content,
(SUM(case when field = 'sessions' then value else null end)) as Sessions,
(SUM(case when field = 'users' then value else null end)) as Users,
(SUM(case when field = 'newUsers' then value else null end)) as New_Users,
(SUM(case when field = 'avgSessionDuration' then value else null end)) as Avg_Session_Duration,
(SUM(case when field = 'bounces' then value else null end)) as Bounces,
(SUM(case when field = 'pageviews' then value else null end)) as Pageviews,
(SUM(case when field = 'goal1Completions' then value else null end)) as Email_Subscribe,
(SUM(case when field = 'goal2Completions' then value else null end)) as Create_Account,
(SUM(case when field = 'goal5Completions' then value else null end)) as Reserve_Button
FROM
unpaid_media.Googleanalytics2 bt
group by date, channelGrouping, deviceCategory, mobileDeviceInfo, landingPagePath, browser, source ;

