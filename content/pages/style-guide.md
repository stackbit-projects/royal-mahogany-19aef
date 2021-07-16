---
title: Treatment
subtitle: Raw Data Query
seo:
  title: Theme Style Guide
  description: A reference for suggested typographic treatment and styles for your content
  extra:
    - name: 'og:type'
      value: website
      keyName: property
    - name: 'og:title'
      value: Theme Style Guide
      keyName: property
    - name: 'og:description'
      value: >-
        A reference for suggested typographic treatment and styles for your
        content
      keyName: property
    - name: 'og:image'
      value: images/1.jpg
      keyName: property
      relativeUrl: true
    - name: 'twitter:card'
      value: summary_large_image
    - name: 'twitter:title'
      value: Theme Style Guide
    - name: 'twitter:description'
      value: >-
        A reference for suggested typographic treatment and styles for your
        content
    - name: 'twitter:image'
      value: images/1.jpg
      relativeUrl: true
layout: page
---
SELECT DISTINCT
MAIN.TPT_ID_KEY,
MAIN.TREATMENT_KEY,
INGREDIENT_NAME,
INGREDIENT_SHORT,
IDENTIFICATION,
PRODUCT_SYNONYM,
INGREDIENT_CONC,
INGREDIENT_CONC_TOTAL,
INGREDIENT_CONC_UNIT,
FORMULATION_TYPE_CODE,
FORMULATION_TYPE,
ing_dosage_list,
ing_dosage_unit_list,
PRODUCT_DOSE,
product_dose_unit,
appl_codes,
spray_volume_appl,
spray_volume_appl_unit,
application_timing_code,
PRODUCTS_APPL.NUMBER_PRODUCTS_APPL AS products_per_application,
ingredient_count,
number_of_applications,
application_method,
application_timing,
ing_dosage,
ing_dosage_unit,
ai_without_safener
FROM
(SELECT DISTINCT
FT.TPT_ID_KEY,
TRT.TREATMENT_KEY,
MASING.DECODE2 AS INGREDIENT_NAME,
MASING.IOP_VALUE AS INGREDIENT_SHORT,
MASPRO.IDENTIFICATION,
MASPROSYN.SYNONYM_CODE AS PRODUCT_SYNONYM,
MASPRO.AMOUNT_SUM AS INGREDIENT_CONC,
MASPRO.AI_COMPLETE AS INGREDIENT_CONC_TOTAL,
AI_UNIT.CODE_VALUE AS INGREDIENT_CONC_UNIT,
FL_TYPE.CODE_VALUE AS FORMULATION_TYPE_CODE,
FL_TYPE.DECODE1 AS FORMULATION_TYPE,
pro.dosage_ai \* ing_dosage_t.convert_factor as ing_dosage_list,
ing_dosage_unit.code_value as ing_dosage_unit_list,
pro.dosage_form \* mufo.convert_factor AS PRODUCT_DOSE,
dosage_form_unit.code_value as product_dose_unit,
pro.appl_codes,
app_eq.spray_volume_appl \* sv_unit_t.convert_factor as spray_volume_appl,
sv_unit.code_value as spray_volume_appl_unit,
timing_code.code_Value as application_timing_code,
'Calculated Field' as products_per_application,
maspro.no_ingredients as ingredient_count,
trt.no_applications as number_of_applications,
app_method.decode1 as application_method,
timing_code.decode1 as application_timing,
pro.dosage_ai \* ing_dosage_t.convert_factor as ing_dosage,
ing_dosage_unit.code_value as ing_dosage_unit,
maspro.ai_without_safener
FROM SCOUT_INTERNAL.FIELD_TESTING FT
LEFT JOIN SCOUT_INTERNAL.TREATMENT TRT ON TRT.FIELD_TESTING_ID = FT.FIELD_TESTING_ID
JOIN SCOUT_INTERNAL.TREATMENT_ENTRYTYPELEVEL TREETL ON TREETL.TREATMENT_ID = TRT.TREATMENT_ID
JOIN SCOUT_INTERNAL.ENTRYTYPE_LEVEL ETL ON ETL.ENTRYTYPE_LEVEL_ID = TREETL.ENTRYTYPE_LEVEL_ID
JOIN SCOUT_INTERNAL.PRODUCT_DESCRIPTION PRO ON  PRO.ENTRYTYPE_LEVEL_ID = ETL.ENTRYTYPE_LEVEL_ID
JOIN SCOUT_INTERNAL.MASTER_PRODUCT_SYNONYM MASPROSYN ON MASPROSYN.PRODUCT_SYNONYM_ID = PRO.PRODUCT_PRODUCT_SYNONYM_ID
JOIN SCOUT_INTERNAL.MASTER_PRODUCT MASPRO ON MASPRO.PRODUCT_ID = MASPROSYN.PRODUCT_ID
JOIN SCOUT_INTERNAL.MASTER_PRODUCT_INGREDIENT MASPROING ON MASPROING.PRODUCT_ID = MASPRO.PRODUCT_ID
JOIN SCOUT_INTERNAL.MASTER_INGR MASING ON MASING.INGR_ID = MASPROING.INGR_ID
LEFT JOIN SCOUT_INTERNAL.MASTER_CODE AI_UNIT ON AI_UNIT.CODE_ID = MASPRO.AI_UNIT_CODE_ID
LEFT JOIN SCOUT_INTERNAL.MASTER_CODE FL_TYPE ON FL_TYPE.CODE_ID = MASPRO.FORMULATION_TYPE_CODE_ID
LEFT JOIN scout_internal.master_unit mufo ON pro.dosage_form_unit_code_id = mufo.master_unit_id
left join scout_internal.master_code dosage_form_unit on dosage_form_unit.code_id = pro.dosage_form_unit_code_id
join scout_internal.field_timing ftim on ftim.field_testing_id = ft.field_testing_id
join scout_internal.application_equipment app_eq on app_eq.timing_id = ftim.timing_id
LEFT JOIN scout_internal.master_unit sv_unit_t ON app_eq.spray_volume_appl_unit_code_id = sv_unit_t.master_unit_id
left join scout_internal.master_code sv_unit on sv_unit.code_id = app_eq.spray_volume_appl_unit_code_id
left join scout_internal.master_code timing_code on timing_code.code_id = ftim.application_timing_code_id
left join scout_internal.master_code app_method on app_method.code_id = app_eq.method_code_id
LEFT JOIN scout_internal.master_unit ing_dosage_t ON pro.dosage_ai_unit_code_id = ing_dosage_t.master_unit_id
left join scout_internal.master_code ing_dosage_unit on ing_dosage_unit.code_id = pro.dosage_ai_unit_code_id
LEFT JOIN scout_internal.master_unit no_safener_t ON maspro.ai_unit_code_id = no_safener_t.master_unit_id
where ft.tpt_id_key in ('IR08NLDF12P037', 'IR08NLDF12P038', 'IR08NLDF12P039', 'IR11BELSMA0418', 'IR11EURX2RES01', 'IR11EURX2RES02',
'IR11FRAL04BIL1', 'IR11FRAL04GIL1', 'IR11NLDF01P001', 'IR11NLDF01P006', 'IR12BELSMA0401', 'IR12EURX4RES01',
'IR12FRAL07BIL1', 'IR12FRAL07MAS1', 'IR12FRAL52XT01', 'IR14BELSMCZ029', 'IR15POLF093-15', 'IR15POLF094-15',
'IR16BELSMBZ061', 'IR16GBRD04DH01', 'IR16POLF12POCE', 'IR16POLF13POCA', 'IR17BELSMAZ007', 'IR17BELSMAZ008',
'IR17GBRC04STC1', 'IR17GBRC07CP01', 'IR17GBRC07DH01', 'IR17POLF09GRSJ', 'IR17POLF09INHO', 'IR18BELSMOZ029', 'IR18GBRB12MB01',
'IR18NLDF05PX14', 'IR18POLF06A1SJ', 'IR18POLF07INH1', 'IR18POLF07INH2', 'IR18POLF08INH1', 'IR18ROU013CM13', 'IR19ESP250EX01', 'IR19ESP250EX02', 'IR19POLF04BCS1')
) MAIN
LEFT JOIN(
SELECT DISTINCT FT.TPT_ID_KEY, TRT.TREATMENT_KEY, COUNT(DISTINCT MASING.INGREDIENT) AS NUMBER_PRODUCTS_APPL
FROM SCOUT_INTERNAL.FIELD_TESTING FT
JOIN SCOUT_INTERNAL.TREATMENT TRT ON TRT.FIELD_TESTING_ID = FT.FIELD_TESTING_ID
JOIN SCOUT_INTERNAL.TREATMENT_ENTRYTYPELEVEL TREETL ON TREETL.TREATMENT_ID = TRT.TREATMENT_ID
JOIN SCOUT_INTERNAL.ENTRYTYPE_LEVEL ETL ON ETL.ENTRYTYPE_LEVEL_ID = TREETL.ENTRYTYPE_LEVEL_ID
JOIN SCOUT_INTERNAL.PRODUCT_DESCRIPTION PRO ON  PRO.ENTRYTYPE_LEVEL_ID = ETL.ENTRYTYPE_LEVEL_ID
JOIN SCOUT_INTERNAL.MASTER_PRODUCT_SYNONYM MASPROSYN ON MASPROSYN.PRODUCT_SYNONYM_ID = PRO.PRODUCT_PRODUCT_SYNONYM_ID
JOIN SCOUT_INTERNAL.MASTER_PRODUCT MASPRO ON MASPRO.PRODUCT_ID = MASPROSYN.PRODUCT_ID
JOIN SCOUT_INTERNAL.MASTER_PRODUCT_INGREDIENT MASPROING ON MASPROING.PRODUCT_ID = MASPRO.PRODUCT_ID
JOIN SCOUT_INTERNAL.MASTER_INGR MASING ON MASING.INGR_ID = MASPROING.INGR_ID
where ft.tpt_id_key in ('IR08NLDF12P037', 'IR08NLDF12P038', 'IR08NLDF12P039', 'IR11BELSMA0418', 'IR11EURX2RES01', 'IR11EURX2RES02',
'IR11FRAL04BIL1', 'IR11FRAL04GIL1', 'IR11NLDF01P001', 'IR11NLDF01P006', 'IR12BELSMA0401', 'IR12EURX4RES01',
'IR12FRAL07BIL1', 'IR12FRAL07MAS1', 'IR12FRAL52XT01', 'IR14BELSMCZ029', 'IR15POLF093-15', 'IR15POLF094-15',
'IR16BELSMBZ061', 'IR16GBRD04DH01', 'IR16POLF12POCE', 'IR16POLF13POCA', 'IR17BELSMAZ007', 'IR17BELSMAZ008',
'IR17GBRC04STC1', 'IR17GBRC07CP01', 'IR17GBRC07DH01', 'IR17POLF09GRSJ', 'IR17POLF09INHO', 'IR18BELSMOZ029', 'IR18GBRB12MB01',
'IR18NLDF05PX14', 'IR18POLF06A1SJ', 'IR18POLF07INH1', 'IR18POLF07INH2', 'IR18POLF08INH1', 'IR18ROU013CM13', 'IR19ESP250EX01', 'IR19ESP250EX02', 'IR19POLF04BCS1')
group by ft.tpt_id_key, trt.treatment_key
) PRODUCTS_APPL ON PRODUCTS_APPL.TPT_ID_KEY = MAIN.TPT_ID_KEY AND PRODUCTS_APPL.TREATMENT_KEY = MAIN.TREATMENT_KEY
