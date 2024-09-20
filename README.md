# DAY-NULM-Dashboard
*In this project, I designed an interactive dashboard with multiple tables, including SHGs, beneficiaries, ALF, CLF, states_UTs, states_zones, districts, ULBs, and more. My team and I imported data based on specific requirements and then wrote optimized queries to retrieve relevant data. This process enabled us to build a dynamic and interactive dashboard that provides clear insights for decision-making.*
SELECT
    b.beneficiary_id,
    bcgw.gender AS gender_category,
    bccw.community AS community_category,
    bcc.caste AS caste_category,
    s.shg_id,
    s.shg_category_id,
    s.shg_sub_id,
    a.alf_id,
    c.clf_id,
    u.ulb_id,
    u.ulb_name,
    d.district_id,
    d.district_name,
    st.state_id,
    st.state_name,
    sz.sz_id,
    sz.zone_name AS state_zone_name,
	s.total_savings AS shg_total_savings,
	s.loan_amount AS shg_loan_amount,
	s.monthly_savings AS shg_monthly_savings,
	s.training_received AS shg_training_received,
	s.no_of_members,
	s.training_received,
	pc.name AS Parliamentary_Name,
	ac.name AS Assembly_Name,
	sc.category AS shg_category,
	ssc.sub_category AS shg_sub_category,
    b.beneficiary_age,
    st.rf_received,
	st.fund_allocated,
	st.fund_utilized,
	st.target_beneficiary,
	st.achieved_beneficiary,
	st.bank_linkage_1,
	st.bank_linkage_2,
	st.bank_linkage_3
FROM
    beneficiary b
LEFT JOIN
    beneficiary_category_gender_wise bcgw ON b.beneficiary_category_gender_wise_id = bcgw.gender_id
LEFT JOIN
    beneficiary_category_community_wise bccw ON b.beneficiary_category_community_wise_id = bccw.community_id
LEFT JOIN
    beneficiary_category_caste_wise bcc ON b.beneficiary_category_caste_wise_id = bcc.caste_id
LEFT JOIN
    shgs s ON b.sgh_id = s.shg_id
LEFT JOIN 
	shg_category sc ON s.shg_category_id = sc.shg_category_id
LEFT JOIN
	shg_sub_category ssc ON s.shg_sub_id = ssc.shg_sub_id
LEFT JOIN
    alf a ON s.alf_id = a.alf_id
LEFT JOIN
    clf c ON a.clf_id = c.clf_id
LEFT JOIN
    ulbs u ON c.ulb_id = u.ulb_id
LEFT JOIN
    wards w ON u.ulb_id = w.ulb_id
LEFT JOIN
    parliamentry_constituencies pc ON w.pc_id = pc.pc_id
LEFT JOIN
    assembly_constituencies ac ON w.ac_id = ac.ac_id
LEFT JOIN
    districts d ON u.district_id = d.district_id
LEFT JOIN
    states_uts st ON d.state_id = st.state_id
LEFT JOIN
    state_zones sz ON st.sz_id = sz.sz_id
	where s.ward_id= w.ward_id
