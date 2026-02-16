# RSB_Tax-Invoice-Form
Tax Invoice Adobe Form
Service Definition

@EndUserText.label: 'Service Defination for Plant LUT'
define service ZUI_ZSDPLANTLUT_M {
  expose ZC_ZSDPLANTLUT_M;
}
***************************************************

Behaviour Definitions

projection;
strict ( 2 );

define behavior for ZC_ZSDPLANTLUT_M //alias <alias_name>
{
  use create;
  use update;
  use delete;
}
*************************************************************

managed implementation in class zbp_i_zsdplantlut_m unique;
strict ( 2 );

define behavior for ZI_ZSDPLANTLUT_M //alias <alias_name>
persistent table zsdplantlut
lock master
authorization master ( instance )
//etag master <field_name>
{
  create;
  update;
  delete;
}
******************************************************************

Data Definitions

@AccessControl.authorizationCheck: #NOT_REQUIRED
@EndUserText.label: 'Consumption View for Plant LUT'
@Metadata.ignorePropagatedAnnotations: true
@Metadata.allowExtensions: true
define root view entity ZC_ZSDPLANTLUT_M
  provider contract transactional_query
  as projection on ZI_ZSDPLANTLUT_M

{
  key Plant,
      Lutno,
      Lutdate,
      Lutvalidity

}
**********************************************************

@AccessControl.authorizationCheck: #NOT_REQUIRED
@EndUserText.label: 'Root view for Plant LUT'
@Metadata.ignorePropagatedAnnotations: true
define root view entity ZI_ZSDPLANTLUT_M
  as select from zsdplantlut
{
  key plant       as Plant,
      lutno       as Lutno,
      lutdate     as Lutdate,
      lutvalidity as Lutvalidity
}
**********************************************************

Strcutures

@EndUserText.label : 'Plant Wise LUT Mapping Data'
@AbapCatalog.enhancement.category : #NOT_EXTENSIBLE
define structure zsdplantlut_data {

  @EndUserText.label : 'LUT No'
  lutno       : abap.char(15);
  lutdate     : dats;
  @EndUserText.label : 'LUT Validity'
  lutvalidity : abap.char(10);

}
**********************************************

@EndUserText.label : 'Plant Wise LUT Mapping Key Fields'
@AbapCatalog.enhancement.category : #NOT_EXTENSIBLE
define structure zsdplantlut_key {

  key client : mandt not null;
  key plant  : werks_d not null;

}
***********************************************************

Classes 

CLASS zbp_i_zsdplantlut_m DEFINITION PUBLIC ABSTRACT FINAL FOR BEHAVIOR OF zi_zsdplantlut_m.
ENDCLASS.

CLASS zbp_i_zsdplantlut_m IMPLEMENTATION.
ENDCLASS.
*******************
managed implementation in class zbp_i_zsdplantlut_m unique;
strict ( 2 );

define behavior for ZI_ZSDPLANTLUT_M //alias <alias_name>
persistent table zsdplantlut
lock master
authorization master ( instance )
//etag master <field_name>
{
  create;
  update;
  delete;
}
************************************************************

class ZCL_ZEXPORTTAXINV_DPC definition
  public
  inheriting from CL_FDP_V3_BD_STAND_GEN_DPC_EXT
  abstract
  create public .

public section.
protected section.
private section.
ENDCLASS.



CLASS ZCL_ZEXPORTTAXINV_DPC IMPLEMENTATION.
ENDCLASS.

***********
class CL_FDP_V3_BD_STAND_GEN_DPC_EXT definition
  public
  inheriting from CL_FDP_V3_BD_STAND_GEN_DPC
  create public .

public section.

  methods /IWBEP/IF_MGW_APPL_SRV_RUNTIME~GET_ENTITY
    redefinition .
  methods /IWBEP/IF_MGW_APPL_SRV_RUNTIME~GET_ENTITYSET
    redefinition .
protected section.

  methods ISRPRINTDETAILS_GET_ENTITY
    importing
      !IV_ENTITY_NAME type STRING
      !IV_ENTITY_SET_NAME type STRING
      !IV_SOURCE_NAME type STRING
      !IT_KEY_TAB type /IWBEP/T_MGW_NAME_VALUE_PAIR
      !IO_REQUEST_OBJECT type ref to /IWBEP/IF_MGW_REQ_ENTITY optional
      !IO_TECH_REQUEST_CONTEXT type ref to /IWBEP/IF_MGW_REQ_ENTITY optional
      !IT_NAVIGATION_PATH type /IWBEP/T_MGW_NAVIGATION_PATH
    exporting
      !ER_ENTITY type DATA
      !ES_RESPONSE_CONTEXT type /IWBEP/IF_MGW_APPL_SRV_RUNTIME=>TY_S_MGW_RESPONSE_ENTITY_CNTXT
    raising
      /IWBEP/CX_MGW_BUSI_EXCEPTION
      /IWBEP/CX_MGW_TECH_EXCEPTION .
  methods ITEMDIFFERENCE_GET_ENTITYSET
    importing
      !IV_ENTITY_NAME type STRING
      !IV_ENTITY_SET_NAME type STRING
      !IV_SOURCE_NAME type STRING
      !IT_FILTER_SELECT_OPTIONS type /IWBEP/T_MGW_SELECT_OPTION
      !IS_PAGING type /IWBEP/S_MGW_PAGING
      !IT_KEY_TAB type /IWBEP/T_MGW_NAME_VALUE_PAIR
      !IT_NAVIGATION_PATH type /IWBEP/T_MGW_NAVIGATION_PATH
      !IT_ORDER type /IWBEP/T_MGW_SORTING_ORDER
      !IV_FILTER_STRING type STRING
      !IV_SEARCH_STRING type STRING
      !IO_TECH_REQUEST_CONTEXT type ref to /IWBEP/IF_MGW_REQ_ENTITYSET optional
    exporting
      !ET_ENTITYSET type DATA
      !ES_RESPONSE_CONTEXT type /IWBEP/IF_MGW_APPL_SRV_RUNTIME=>TY_S_MGW_RESPONSE_CONTEXT
    raising
      /IWBEP/CX_MGW_BUSI_EXCEPTION
      /IWBEP/CX_MGW_TECH_EXCEPTION .
  methods ITEMPRICINGDIFF_GET_ENTITYSET
    importing
      !IV_ENTITY_NAME type STRING
      !IV_ENTITY_SET_NAME type STRING
      !IV_SOURCE_NAME type STRING
      !IT_FILTER_SELECT_OPTIONS type /IWBEP/T_MGW_SELECT_OPTION
      !IS_PAGING type /IWBEP/S_MGW_PAGING
      !IT_KEY_TAB type /IWBEP/T_MGW_NAME_VALUE_PAIR
      !IT_NAVIGATION_PATH type /IWBEP/T_MGW_NAVIGATION_PATH
      !IT_ORDER type /IWBEP/T_MGW_SORTING_ORDER
      !IV_FILTER_STRING type STRING
      !IV_SEARCH_STRING type STRING
      !IO_TECH_REQUEST_CONTEXT type ref to /IWBEP/IF_MGW_REQ_ENTITYSET optional
    exporting
      !ET_ENTITYSET type CL_FDP_V3_BD_STAND_GEN_MPC=>TT_ITEMPRICINGDIFFERENCENODE
      !ES_RESPONSE_CONTEXT type /IWBEP/IF_MGW_APPL_SRV_RUNTIME=>TY_S_MGW_RESPONSE_CONTEXT
    raising
      /IWBEP/CX_MGW_BUSI_EXCEPTION
      /IWBEP/CX_MGW_TECH_EXCEPTION .
  methods ITEMAFTERCORR_GET_ENTITYSET
    importing
      !IV_ENTITY_NAME type STRING
      !IV_ENTITY_SET_NAME type STRING
      !IV_SOURCE_NAME type STRING
      !IT_FILTER_SELECT_OPTIONS type /IWBEP/T_MGW_SELECT_OPTION
      !IS_PAGING type /IWBEP/S_MGW_PAGING
      !IT_KEY_TAB type /IWBEP/T_MGW_NAME_VALUE_PAIR
      !IT_NAVIGATION_PATH type /IWBEP/T_MGW_NAVIGATION_PATH
      !IT_ORDER type /IWBEP/T_MGW_SORTING_ORDER
      !IV_FILTER_STRING type STRING
      !IV_SEARCH_STRING type STRING
      !IO_TECH_REQUEST_CONTEXT type ref to /IWBEP/IF_MGW_REQ_ENTITYSET optional
    exporting
      !ET_ENTITYSET type DATA
      !ES_RESPONSE_CONTEXT type /IWBEP/IF_MGW_APPL_SRV_RUNTIME=>TY_S_MGW_RESPONSE_CONTEXT
    raising
      /IWBEP/CX_MGW_BUSI_EXCEPTION
      /IWBEP/CX_MGW_TECH_EXCEPTION .
  methods ITEMPRICAFTCORR_GET_ENTITYSET
    importing
      !IV_ENTITY_NAME type STRING
      !IV_ENTITY_SET_NAME type STRING
      !IV_SOURCE_NAME type STRING
      !IT_FILTER_SELECT_OPTIONS type /IWBEP/T_MGW_SELECT_OPTION
      !IS_PAGING type /IWBEP/S_MGW_PAGING
      !IT_KEY_TAB type /IWBEP/T_MGW_NAME_VALUE_PAIR
      !IT_NAVIGATION_PATH type /IWBEP/T_MGW_NAVIGATION_PATH
      !IT_ORDER type /IWBEP/T_MGW_SORTING_ORDER
      !IV_FILTER_STRING type STRING
      !IV_SEARCH_STRING type STRING
      !IO_TECH_REQUEST_CONTEXT type ref to /IWBEP/IF_MGW_REQ_ENTITYSET optional
    exporting
      !ET_ENTITYSET type CL_FDP_V3_BD_STAND_GEN_MPC=>TT_ITEMPRICINGAFTERCORRNODE
      !ES_RESPONSE_CONTEXT type /IWBEP/IF_MGW_APPL_SRV_RUNTIME=>TY_S_MGW_RESPONSE_CONTEXT
    raising
      /IWBEP/CX_MGW_BUSI_EXCEPTION
      /IWBEP/CX_MGW_TECH_EXCEPTION .
  methods CLEAREDDOWNPAYT_GET_ENTITYSET
    importing
      !IV_ENTITY_NAME type STRING
      !IV_ENTITY_SET_NAME type STRING
      !IV_SOURCE_NAME type STRING
      !IT_FILTER_SELECT_OPTIONS type /IWBEP/T_MGW_SELECT_OPTION
      !IS_PAGING type /IWBEP/S_MGW_PAGING
      !IT_KEY_TAB type /IWBEP/T_MGW_NAME_VALUE_PAIR
      !IT_NAVIGATION_PATH type /IWBEP/T_MGW_NAVIGATION_PATH
      !IT_ORDER type /IWBEP/T_MGW_SORTING_ORDER
      !IV_FILTER_STRING type STRING
      !IV_SEARCH_STRING type STRING
      !IO_TECH_REQUEST_CONTEXT type ref to /IWBEP/IF_MGW_REQ_ENTITYSET optional
    exporting
      !ET_ENTITYSET type CL_FDP_V3_BD_STAND_GEN_MPC=>TT_CLEAREDDOWNPAYMENTNODE
      !ES_RESPONSE_CONTEXT type /IWBEP/IF_MGW_APPL_SRV_RUNTIME=>TY_S_MGW_RESPONSE_CONTEXT .
  methods CLEAREDDOWNPAYTOVW_GET_ENTITY
    importing
      !IV_ENTITY_NAME type STRING
      !IV_ENTITY_SET_NAME type STRING
      !IV_SOURCE_NAME type STRING
      !IT_KEY_TAB type /IWBEP/T_MGW_NAME_VALUE_PAIR
      !IO_REQUEST_OBJECT type ref to /IWBEP/IF_MGW_REQ_ENTITY optional
      !IO_TECH_REQUEST_CONTEXT type ref to /IWBEP/IF_MGW_REQ_ENTITY optional
      !IT_NAVIGATION_PATH type /IWBEP/T_MGW_NAVIGATION_PATH
    exporting
      !ER_ENTITY type CL_FDP_V3_BD_STAND_GEN_MPC=>TS_CLEAREDDOWNPAYMENTNODE
      !ES_RESPONSE_CONTEXT type /IWBEP/IF_MGW_APPL_SRV_RUNTIME=>TY_S_MGW_RESPONSE_ENTITY_CNTXT .
  methods OPENDOWNPAYT_GET_ENTITY
    importing
      !IV_ENTITY_NAME type STRING
      !IV_ENTITY_SET_NAME type STRING
      !IV_SOURCE_NAME type STRING
      !IT_KEY_TAB type /IWBEP/T_MGW_NAME_VALUE_PAIR
      !IO_REQUEST_OBJECT type ref to /IWBEP/IF_MGW_REQ_ENTITY optional
      !IO_TECH_REQUEST_CONTEXT type ref to /IWBEP/IF_MGW_REQ_ENTITY optional
      !IT_NAVIGATION_PATH type /IWBEP/T_MGW_NAVIGATION_PATH
    exporting
      !ER_ENTITY type CL_FDP_V3_BD_STAND_GEN_MPC=>TS_OPENDOWNPAYMENTNODE
      !ES_RESPONSE_CONTEXT type /IWBEP/IF_MGW_APPL_SRV_RUNTIME=>TY_S_MGW_RESPONSE_ENTITY_CNTXT .
  methods SUPPLIER_GET_ENTITY
    importing
      !IV_ENTITY_NAME type STRING
      !IV_ENTITY_SET_NAME type STRING
      !IV_SOURCE_NAME type STRING
      !IT_KEY_TAB type /IWBEP/T_MGW_NAME_VALUE_PAIR
      !IO_REQUEST_OBJECT type ref to /IWBEP/IF_MGW_REQ_ENTITY optional
      !IO_TECH_REQUEST_CONTEXT type ref to /IWBEP/IF_MGW_REQ_ENTITY optional
      !IT_NAVIGATION_PATH type /IWBEP/T_MGW_NAVIGATION_PATH
    exporting
      !ER_ENTITY type CL_FDP_V3_BD_STAND_GEN_MPC=>TS_SUPPLIERNODE
      !ES_RESPONSE_CONTEXT type /IWBEP/IF_MGW_APPL_SRV_RUNTIME=>TY_S_MGW_RESPONSE_ENTITY_CNTXT .

  methods BILLINGDOCUMEN02_GET_ENTITYSET
    redefinition .
  methods COMPANY_GET_ENTITY
    redefinition .
  methods INVOICEITEMSET_GET_ENTITYSET
    redefinition .
  methods INVOICESET_GET_ENTITY
    redefinition .
  methods ITEMPRICECONDITI_GET_ENTITYSET
    redefinition .
  methods LEGALLYREQUIREDT_GET_ENTITYSET
    redefinition .
  methods PARTYADDRESSSET_GET_ENTITY
    redefinition .
  methods PRICECONDITIONSE_GET_ENTITYSET
    redefinition .
  methods SEPASET_GET_ENTITY
    redefinition .
  methods SERIALNUMBER_GET_ENTITYSET
    redefinition .
  methods SERVICERECIPIENT_GET_ENTITY
    redefinition .
  methods TAXATIONTERMSSET_GET_ENTITY
    redefinition .
  methods VATSUMMARY_GET_ENTITYSET
    redefinition .
private section.

  data MS_BILLING_DOCUMENT type CL_FDP_V3_BD_FORM_UTILITY=>TY_BILLING_DOCUMENT .
  data MV_LANGUAGE type SY-LANGU .
  data MV_SENDER_COUNTRY type LAND1 .
  data MT_ITEM_DIFFERENCE type CL_GLO_LOG_FORM_UTILITY=>TY_T_ITEM .
  data MT_ITEM_PRICING_DIFFERENCE type CL_GLO_LOG_FORM_UTILITY=>TY_T_ITEM_PRICING .
  data MT_ITEM_PRICE_CONDITIONS type CL_FDP_V3_BD_FORM_UTILITY=>TT_PRICE_CONDITIONS .
  data MT_ITEM_AFTER_CORRECTION type CL_GLO_LOG_FORM_UTILITY=>TY_T_ITEM .
  data MT_ITEM_PRICING_AFTERCORR type CL_GLO_LOG_FORM_UTILITY=>TY_T_ITEM_PRICING .
  data MV_CORRECTION_INDICATOR type BOOLE_D .
  data MT_CLEARED_DOWNPAYMENT type CL_FDP_V3_BD_STAND_GEN_MPC=>TT_CLEAREDDOWNPAYMENTNODE .
  data MS_CLEARED_DOWNPAYMENT_OVW type CL_FDP_V3_BD_STAND_GEN_MPC=>TS_CLEAREDDOWNPAYMENTNODE .
  data MV_DOWNPAYMENT_TEXT type CHAR120 .
  data MT_ITEM_DELIVERY_REF type CL_FDP_V3_BD_FORM_UTILITY=>TT_DELIVERY_REF .
  data MT_ITEM_SALESORDER_REF type CL_FDP_V3_BD_FORM_UTILITY=>TT_SALESORDER_REF .
  data MT_SERIAL_NUMBERS type RSEROB_T .
  data MT_BILLING_DOCUMENT_ITEM type CL_GLO_LOG_FORM_UTILITY=>TY_T_ITEM .

  methods FILL_SERIAL_NUMBERS .
  methods SET_BILLING_DOCUMENT_ITEM
    importing
      !IV_BILLING_DOCUMENT type VBELN .
ENDCLASS.



CLASS CL_FDP_V3_BD_STAND_GEN_DPC_EXT IMPLEMENTATION.


  METHOD /iwbep/if_mgw_appl_srv_runtime~get_entity.

    CONSTANTS : lc_country_ch TYPE string VALUE 'CH',
                lc_country_pl TYPE string VALUE 'PL',
                lc_country_in TYPE string VALUE 'IN',
                lc_country_ae TYPE string VALUE 'AE',
                lc_country_om TYPE string VALUE 'OM',
                lc_country_sa TYPE string VALUE 'SA',
                lc_country_eg TYPE string VALUE 'EG'.

    DATA: ls_isrprintdetails TYPE cl_fdp_v3_bd_stand_gen_mpc=>ts_isrprintdetailsnode,
          ls_clearedDownpaymentOvw TYPE cl_fdp_v3_bd_stand_gen_mpc=>TS_CLEAREDDOWNPAYMENTNODE,
          ls_openDownpayment TYPE cl_fdp_v3_bd_stand_gen_mpc=>TS_OPENDOWNPAYMENTNODE,
          ls_supplier  TYPE cl_fdp_v3_bd_stand_gen_mpc=>ts_suppliernode,
          ls_billtoparty TYPE cl_fdp_v3_bd_stand_gen_mpc=>TS_BILLTOPARTYNODE,
          ls_shiptoparty TYPE cl_fdp_v3_bd_stand_gen_mpc=>TS_SHIPTOPARTYNODE.

    IF ms_billing_document IS INITIAL.
      CALL METHOD get_billing_document
        RECEIVING
          rs_billing_document = ms_billing_document.
    ENDIF.

    IF iv_entity_name = 'ISRPrintDetailsNode'.
      IF ms_billing_document-landtx = lc_country_ch.
        TRY.
            CALL METHOD me->isrprintdetails_get_entity
              EXPORTING
                iv_entity_name      = iv_entity_name
                iv_entity_set_name  = iv_entity_set_name
                iv_source_name      = iv_source_name
                it_key_tab          = it_key_tab
                it_navigation_path  = it_navigation_path
              IMPORTING
                er_entity           = ls_isrprintdetails
                es_response_context = es_response_context.
          CATCH /iwbep/cx_mgw_busi_exception .
          CATCH /iwbep/cx_mgw_tech_exception .
        ENDTRY.

*      Send specific entity data to the caller interface
        copy_data_to_ref(
          EXPORTING
            is_data = ls_isrprintdetails
          CHANGING
            cr_data = er_entity ).

      ENDIF.
      ELSEIF iv_entity_name = 'ClearedDownPaymentOvwNode'.
      IF ms_billing_document-landtx = lc_country_pl.
        TRY.
            CALL METHOD me->cleareddownpaytovw_get_entity
              EXPORTING
                iv_entity_name      = iv_entity_name
                iv_entity_set_name  = iv_entity_set_name
                iv_source_name      = iv_source_name
                it_key_tab          = it_key_tab
                it_navigation_path  = it_navigation_path
              IMPORTING
                er_entity           = ls_clearedDownpaymentOvw
                es_response_context = es_response_context.
          CATCH /iwbep/cx_mgw_busi_exception .
          CATCH /iwbep/cx_mgw_tech_exception .
        ENDTRY.

*      Send specific entity data to the caller interface
        copy_data_to_ref(
          EXPORTING
            is_data = ls_clearedDownpaymentOvw
          CHANGING
            cr_data = er_entity ).

      ENDIF.
          ELSEIF iv_entity_name = 'OpenDownPaymentNode'.
      IF ms_billing_document-landtx = lc_country_pl.
        TRY.
            CALL METHOD me->opendownpayt_get_entity
              EXPORTING
                iv_entity_name      = iv_entity_name
                iv_entity_set_name  = iv_entity_set_name
                iv_source_name      = iv_source_name
                it_key_tab          = it_key_tab
                it_navigation_path  = it_navigation_path
              IMPORTING
                er_entity           = ls_openDownpayment
                es_response_context = es_response_context.
          CATCH /iwbep/cx_mgw_busi_exception .
          CATCH /iwbep/cx_mgw_tech_exception .
        ENDTRY.

*      Send specific entity data to the caller interface
        copy_data_to_ref(
          EXPORTING
            is_data = ls_openDownpayment
          CHANGING
            cr_data = er_entity ).

      ENDIF.

    ELSEIF iv_entity_name = 'SupplierNode'.

      IF ms_billing_document-landtx = lc_country_in.

        TRY.
          CALL METHOD me->supplier_get_entity
            EXPORTING
              iv_entity_name          = iv_entity_name
              iv_entity_set_name      = iv_entity_set_name
              iv_source_name          = iv_source_name
              it_key_tab              = it_key_tab
              it_navigation_path      = it_navigation_path
            IMPORTING
              er_entity               = ls_supplier
              es_response_context     = es_response_context
              .
          CATCH /iwbep/cx_mgw_busi_exception .
          CATCH /iwbep/cx_mgw_tech_exception .
        ENDTRY.

*       Send specific entity data to the caller interface
        copy_data_to_ref(
          EXPORTING
            is_data = ls_supplier
          CHANGING
            cr_data = er_entity ).

      ENDIF.
"1908 HFC02 UAE/KSA Customer Invoice Forms
"2005 IN billTo Address correction
      ELSEIF iv_entity_name = 'BillToPartyNode' AND ( ms_billing_document-landtx = lc_country_sa OR ms_billing_document-landtx = lc_country_ae OR ms_billing_document-landtx = lc_country_in
                                                      OR ms_billing_document-landtx = lc_country_eg OR ms_billing_document-landtx = lc_country_om ).

"      IF ms_billing_document-landtx = lc_country_sa OR
"         ms_billing_document-landtx = lc_country_ae.


        TRY.
          CALL METHOD me->partyaddressset_get_entity
            EXPORTING
              iv_entity_name          = iv_entity_name
              iv_entity_set_name      = iv_entity_set_name
              iv_source_name          = iv_source_name
              it_key_tab              = it_key_tab
              it_navigation_path      = it_navigation_path
            IMPORTING
              er_entity               = ls_billtoparty
              es_response_context     = es_response_context
              .
          CATCH /iwbep/cx_mgw_busi_exception .
          CATCH /iwbep/cx_mgw_tech_exception .
        ENDTRY.

*       Send specific entity data to the caller interface
        copy_data_to_ref(
          EXPORTING
            is_data = ls_billtoparty
          CHANGING
            cr_data = er_entity ).

"      ENDIF.

     ELSEIF iv_entity_name = 'ShipToPartyNode' AND ( ms_billing_document-landtx = lc_country_in ).

        TRY.
          CALL METHOD me->servicerecipient_get_entity
            EXPORTING
              iv_entity_name          = iv_entity_name
              iv_entity_set_name      = iv_entity_set_name
              iv_source_name          = iv_source_name
              it_key_tab              = it_key_tab
              it_navigation_path      = it_navigation_path
            IMPORTING
              er_entity               = ls_shiptoparty
              es_response_context     = es_response_context
              .
          CATCH /iwbep/cx_mgw_busi_exception .
          CATCH /iwbep/cx_mgw_tech_exception .
        ENDTRY.

*       Send specific entity data to the caller interface
        copy_data_to_ref(
          EXPORTING
            is_data = ls_shiptoparty
          CHANGING
            cr_data = er_entity ).
     ELSE.
      TRY.
          CALL METHOD super->/iwbep/if_mgw_appl_srv_runtime~get_entity
            EXPORTING
              iv_entity_name          = iv_entity_name
              iv_entity_set_name      = iv_entity_set_name
              iv_source_name          = iv_source_name
              it_key_tab              = it_key_tab
              it_navigation_path      = it_navigation_path
              io_tech_request_context = io_tech_request_context
            IMPORTING
              er_entity               = er_entity
              es_response_context     = es_response_context.
        CATCH /iwbep/cx_mgw_busi_exception .
        CATCH /iwbep/cx_mgw_tech_exception .

      ENDTRY.
    ENDIF.
  ENDMETHOD.


  METHOD /iwbep/if_mgw_appl_srv_runtime~get_entityset.

    CONSTANTS : lc_country_pl TYPE string VALUE 'PL'.

    DATA: lt_itemdifferencenode        TYPE cl_fdp_v3_bd_stand_gen_mpc=>tt_itemdifferencenode,
          lt_itempricingdifferencenode TYPE cl_fdp_v3_bd_stand_gen_mpc=>tt_itempricingdifferencenode,
          lt_itempricingaftercorrnode  TYPE cl_fdp_v3_bd_stand_gen_mpc=>tt_itempricingaftercorrnode,
          lt_itemaftercorrnode         TYPE cl_fdp_v3_bd_stand_gen_mpc=>tt_itemaftercorrnode,
          lt_clearedDownpayment        TYPE cl_fdp_v3_bd_stand_gen_mpc=>TT_CLEAREDDOWNPAYMENTNODE.


    IF ms_billing_document IS INITIAL.
      CALL METHOD get_billing_document
        RECEIVING
          rs_billing_document = ms_billing_document.
    ENDIF.



    CASE iv_entity_name.
      WHEN 'ItemDifferenceNode'.
        IF ms_billing_document-landtx = lc_country_pl
                 AND ms_billing_document-vbtyp NE 'M'.      " Correction Invoice

          TRY.
              CALL METHOD me->itemdifference_get_entityset
                EXPORTING
                  iv_entity_name           = iv_entity_name
                  iv_entity_set_name       = iv_entity_set_name
                  iv_source_name           = iv_source_name
                  it_filter_select_options = it_filter_select_options
                  is_paging                = is_paging
                  it_key_tab               = it_key_tab
                  it_navigation_path       = it_navigation_path
                  it_order                 = it_order
                  iv_filter_string         = iv_filter_string
                  iv_search_string         = iv_search_string
                  io_tech_request_context  = io_tech_request_context
                IMPORTING
                  et_entityset             = lt_itemdifferencenode
                  es_response_context      = es_response_context.
            CATCH /iwbep/cx_mgw_busi_exception .
            CATCH /iwbep/cx_mgw_tech_exception .
          ENDTRY.


*      Send specific entity data to the caller interface
          copy_data_to_ref(
            EXPORTING
              is_data = lt_itemdifferencenode
            CHANGING
              cr_data = er_entityset ).

        ENDIF.

      WHEN 'ItemPricingDifferenceNode'.
        IF ms_billing_document-landtx = lc_country_pl
                  AND ms_billing_document-vbtyp NE 'M'.      " Correction Invoice

          TRY.
              CALL METHOD me->itempricingdiff_get_entityset
                EXPORTING
                  iv_entity_name           = iv_entity_name
                  iv_entity_set_name       = iv_entity_set_name
                  iv_source_name           = iv_source_name
                  it_filter_select_options = it_filter_select_options
                  is_paging                = is_paging
                  it_key_tab               = it_key_tab
                  it_navigation_path       = it_navigation_path
                  it_order                 = it_order
                  iv_filter_string         = iv_filter_string
                  iv_search_string         = iv_search_string
                  io_tech_request_context  = io_tech_request_context
                IMPORTING
                  et_entityset             = lt_itempricingdifferencenode
                  es_response_context      = es_response_context.
            CATCH /iwbep/cx_mgw_busi_exception .
            CATCH /iwbep/cx_mgw_tech_exception .
          ENDTRY.

*              Send specific entity data to the caller interface
          copy_data_to_ref(
            EXPORTING
              is_data = lt_itempricingdifferencenode
            CHANGING
              cr_data = er_entityset ).
        ENDIF.

      WHEN 'ItemPricingAfterCorrNode'.
         IF ms_billing_document-landtx = lc_country_pl
                  AND ms_billing_document-vbtyp NE 'M'.      " Correction Invoice

          TRY.
              CALL METHOD me->itempricaftcorr_get_entityset
                EXPORTING
                  iv_entity_name           = iv_entity_name
                  iv_entity_set_name       = iv_entity_set_name
                  iv_source_name           = iv_source_name
                  it_filter_select_options = it_filter_select_options
                  is_paging                = is_paging
                  it_key_tab               = it_key_tab
                  it_navigation_path       = it_navigation_path
                  it_order                 = it_order
                  iv_filter_string         = iv_filter_string
                  iv_search_string         = iv_search_string
                  io_tech_request_context  = io_tech_request_context
                IMPORTING
                  et_entityset             = lt_itempricingaftercorrnode
                  es_response_context      = es_response_context.
            CATCH /iwbep/cx_mgw_busi_exception .
            CATCH /iwbep/cx_mgw_tech_exception .
          ENDTRY.

*              Send specific entity data to the caller interface
          copy_data_to_ref(
            EXPORTING
              is_data = lt_itempricingaftercorrnode
            CHANGING
              cr_data = er_entityset ).
        ENDIF.


      WHEN 'ItemAfterCorrNode'.
        IF ms_billing_document-landtx = lc_country_pl
                  AND ms_billing_document-vbtyp NE 'M'.      " Correction Invoice

          TRY.
              CALL METHOD me->itemaftercorr_get_entityset
                EXPORTING
                  iv_entity_name           = iv_entity_name
                  iv_entity_set_name       = iv_entity_set_name
                  iv_source_name           = iv_source_name
                  it_filter_select_options = it_filter_select_options
                  is_paging                = is_paging
                  it_key_tab               = it_key_tab
                  it_navigation_path       = it_navigation_path
                  it_order                 = it_order
                  iv_filter_string         = iv_filter_string
                  iv_search_string         = iv_search_string
                  io_tech_request_context  = io_tech_request_context
                IMPORTING
                  et_entityset             = lt_itemaftercorrnode
                  es_response_context      = es_response_context.
            CATCH /iwbep/cx_mgw_busi_exception .
            CATCH /iwbep/cx_mgw_tech_exception .
          ENDTRY.


*              Send specific entity data to the caller interface
          copy_data_to_ref(
            EXPORTING
              is_data = lt_itemaftercorrnode
            CHANGING
              cr_data = er_entityset ).
        ENDIF.


       WHEN 'ClearedDownPaymentNode'.
        IF ms_billing_document-landtx = lc_country_pl.

          TRY.
              CALL METHOD me->CLEAREDDOWNPAYT_GET_ENTITYSET
                EXPORTING
                  iv_entity_name           = iv_entity_name
                  iv_entity_set_name       = iv_entity_set_name
                  iv_source_name           = iv_source_name
                  it_filter_select_options = it_filter_select_options
                  is_paging                = is_paging
                  it_key_tab               = it_key_tab
                  it_navigation_path       = it_navigation_path
                  it_order                 = it_order
                  iv_filter_string         = iv_filter_string
                  iv_search_string         = iv_search_string
                  io_tech_request_context  = io_tech_request_context
                IMPORTING
                  et_entityset             = lt_clearedDownpayment
                  es_response_context      = es_response_context.
            CATCH /iwbep/cx_mgw_busi_exception .
            CATCH /iwbep/cx_mgw_tech_exception .
          ENDTRY.


*              Send specific entity data to the caller interface
          copy_data_to_ref(
            EXPORTING
              is_data = lt_clearedDownpayment
            CHANGING
              cr_data = er_entityset ).
        ENDIF.

      WHEN OTHERS.

        TRY.
            CALL METHOD super->/iwbep/if_mgw_appl_srv_runtime~get_entityset
              EXPORTING
                iv_entity_name           = iv_entity_name
                iv_entity_set_name       = iv_entity_set_name
                iv_source_name           = iv_source_name
                it_filter_select_options = it_filter_select_options
                it_order                 = it_order
                is_paging                = is_paging
                it_navigation_path       = it_navigation_path
                it_key_tab               = it_key_tab
                iv_filter_string         = iv_filter_string
                iv_search_string         = iv_search_string
                io_tech_request_context  = io_tech_request_context
              IMPORTING
                er_entityset             = er_entityset
                es_response_context      = es_response_context.
          CATCH /iwbep/cx_mgw_busi_exception .
          CATCH /iwbep/cx_mgw_tech_exception .
        ENDTRY.

    ENDCASE.

  ENDMETHOD.


  METHOD billingdocumen02_get_entityset.
    DATA: ls_bil_doc_key TYPE /iwbep/s_mgw_name_value_pair,
          ls_item_key    TYPE /iwbep/s_mgw_name_value_pair,
          lt_xvbrp       TYPE STANDARD TABLE OF vbrpvb,
          ls_item        TYPE vbrp,
          lt_conf_out    TYPE TABLE OF conf_out,
          ls_entityset   LIKE LINE OF et_entityset,
          lo_data_buffer TYPE REF TO cl_fdp_v3_data_buffer.

    FIELD-SYMBOLS: <fs_conf_out> TYPE conf_out.

    CLEAR: et_entityset,
           es_response_context.

* Sanity Check
    READ TABLE it_key_tab
         WITH KEY name = 'BillingDocument'
         INTO ls_bil_doc_key.

    lo_data_buffer = cl_fdp_v3_bd_form_utility=>get_data_buffer( ).
    ASSERT lo_data_buffer->ms_header-vbeln = ls_bil_doc_key-value.

* Get Data
    READ TABLE it_key_tab
         WITH KEY name = 'BillingDocumentItem'
         INTO ls_item_key.

    READ TABLE lo_data_buffer->mt_item WITH KEY vbeln = lo_data_buffer->ms_header-vbeln posnr = ls_item_key-value REFERENCE INTO DATA(lr_item).

    TEST-SEAM skip_lr.
    ls_item-matnr = lr_item->matnr.
    ls_item-charg = lr_item->charg.
    ls_item-werks = lr_item->werks.
    ls_item-cuobj = lr_item->cuobj.
    END-TEST-SEAM.

    CALL FUNCTION 'VB_BATCH_VALUES_FOR_OUTPUT'
      EXPORTING
        material               = ls_item-matnr
        plant                  = ls_item-werks
        batch                  = ls_item-charg
        batch_cuobj            = ls_item-cuobj
        language               = mv_language
      TABLES
*       objects                =
        classification         = lt_conf_out
      EXCEPTIONS
        no_classification_data = 1
        OTHERS                 = 2.

    TEST-SEAM fill_lt.
    END-TEST-SEAM.

    LOOP AT lt_conf_out ASSIGNING <fs_conf_out>.
      ls_entityset-characteristic = <fs_conf_out>-atnam.
      ls_entityset-characteristic_description = <fs_conf_out>-atbez.
      ls_entityset-characteristic_value = <fs_conf_out>-atwrt.
      ls_entityset-characteristic_value_descript = <fs_conf_out>-atwtb.

      INSERT ls_entityset INTO TABLE et_entityset.
    ENDLOOP.
  ENDMETHOD.


  METHOD cleareddownpaytovw_get_entity.

    DATA: lv_gross_amt           TYPE netwr,
          lv_net_amt             TYPE netwr,
          lv_tax_amt             TYPE netwr,
          wa_cleared_downpayment TYPE cl_fdp_v3_bd_stand_gen_mpc=>ts_cleareddownpaymentnode.

    CLEAR: lv_gross_amt,lv_net_amt,lv_tax_amt,ms_cleared_downpayment_ovw.

    LOOP AT  mt_cleared_downpayment INTO wa_cleared_downpayment.
      lv_gross_amt = lv_gross_amt + wa_cleared_downpayment-downpaymentgrossamount.
      lv_net_amt = lv_net_amt + wa_cleared_downpayment-downpaymentnetamount.
      lv_tax_amt = lv_tax_amt + wa_cleared_downpayment-downpaymenttaxamount.

    ENDLOOP.

    er_entity-downpaymentgrossamount = lv_gross_amt.
    er_entity-downpaymentnetamount = lv_net_amt.
    er_entity-downpaymenttaxamount = lv_tax_amt.
    er_entity-documentdescription = mv_downpayment_text.

    ms_cleared_downpayment_ovw = er_entity.

  ENDMETHOD.


  METHOD cleareddownpayt_get_entityset.

    CONSTANTS : lc_country_pl TYPE string VALUE 'PL'.
    DATA: ls_bil_doc_key TYPE /iwbep/s_mgw_name_value_pair.

    DATA :lt_dwnpayt      TYPE STANDARD TABLE OF  cpldwnpayt,
          lt_dwnpayt_text TYPE STANDARD TABLE OF cpldwnpayt,
          ls_dwnpayt_text TYPE  cpldwnpayt,
          ls_key          TYPE LINE OF /iwbep/t_mgw_name_value_pair,
          ls_dwnpayt      LIKE LINE OF lt_dwnpayt,
          ls_dwnpayt_doc  LIKE LINE OF lt_dwnpayt,
          lv_gross        TYPE wertv8,
          lv_net          TYPE wertv8,
          lv_tax          TYPE wertv8,
          er_billing      TYPE cl_fdp_v3_bd_standard_mpc=>ts_billingdocumentnode,
          ls_entity       TYPE cl_fdp_v3_bd_stand_gen_mpc=>ts_cleareddownpaymentnode,
          lt_entity       TYPE TABLE OF cl_fdp_v3_bd_stand_gen_mpc=>ts_cleareddownpaymentnode,
          ls_curr_entity  TYPE cl_fdp_v3_bd_stand_gen_mpc=>ts_cleareddownpaymentnode,
          lt_curr_entity  like lt_dwnpayt,
          lt_bseg         TYPE STANDARD TABLE OF bseg,
          ls_bseg         TYPE bseg,
          lv_belnr        TYPE vbrk-BELNR,
          lv_tax_proc type kalsm,
          idx type sy-tabix.

    CLEAR: et_entityset,
           es_response_context,
           mv_downpayment_text,
           mt_cleared_downpayment,
           mt_cleared_downpayment.

* Sanity Check
    READ TABLE it_key_tab
         WITH KEY name = 'BillingDocument'
         INTO ls_bil_doc_key.

   TEST-SEAM skip_key.
    ASSERT ms_billing_document-vbeln = ls_bil_doc_key-value.
   END-TEST-SEAM.

    IF ms_billing_document-landtx = lc_country_pl.      " Poland

      SELECT * FROM cpldwnpayt INTO TABLE @lt_dwnpayt WHERE salesdocument EQ @ms_billing_document-vbeln_so.

      READ TABLE lt_dwnpayt INTO ls_curr_entity  WITH KEY billingdocument = ms_billing_document-vbeln.
      IF sy-subrc = 0.

        LOOP AT lt_dwnpayt INTO ls_dwnpayt
         WHERE ( postingdate < ls_curr_entity-postingdate OR
        ( postingdate = ls_curr_entity-postingdate AND creationtime <= ls_curr_entity-creationtime ) ) AND
          downpaymentnetamount >= 0
            GROUP BY ls_dwnpayt-billingdocument.
          ls_dwnpayt_text-billingdocument = ls_dwnpayt-billingdocument.
          APPEND ls_dwnpayt_text TO lt_dwnpayt_text.
          CLEAR ls_dwnpayt_text.
          CLEAR ls_dwnpayt.
        ENDLOOP.

        SORT lt_dwnpayt_text by billingdocument.
        DELETE ADJACENT DUPLICATES FROM lt_dwnpayt_text COMPARING billingdocument.

        LOOP AT lt_dwnpayt_text INTO ls_dwnpayt_text.
          SHIFT ls_dwnpayt_text-billingdocument LEFT DELETING LEADING '0'.
          CONCATENATE mv_downpayment_text ', ' ls_dwnpayt_text-billingdocument INTO mv_downpayment_text.
        ENDLOOP.
        SHIFT mv_downpayment_text LEFT DELETING LEADING ','.


        LOOP AT lt_dwnpayt into ls_curr_entity where billingdocument = ms_billing_document-vbeln.
          APPEND ls_curr_entity to lt_curr_entity.
        ENDLOOP.

        SELECT SINGLE BELNR into lv_belnr from vbrk where vbeln = ms_billing_document-vbeln.

        SELECT * into TABLE lt_bseg from bseg where belnr = lv_belnr AND bukrs = ms_billing_document-bukrs AND buzid = 'T'.   "#EC CI_ALL_FIELDS_NEEDED

        LOOP AT lt_curr_entity into ls_curr_entity.
          READ TABLE lt_bseg INTO ls_bseg with key mwskz = ls_curr_entity-taxcode.
          ls_curr_entity-downpaymentnetamount = -1 * ls_curr_entity-downpaymentnetamount.
          ls_curr_entity-downpaymenttaxamount = ls_curr_entity-downpaymenttaxamount - ls_bseg-wrbtr.
          ls_curr_entity-downpaymentgrossamount = ls_curr_entity-downpaymentnetamount + ls_curr_entity-downpaymenttaxamount.

          APPEND ls_curr_entity to et_entityset.
        ENDLOOP.

          TEST-SEAM ts_tpr.
          END-TEST-SEAM.
          IF lv_tax_proc IS INITIAL.
                  SELECT SINGLE kalsm FROM t005 INTO lv_tax_proc
                          WHERE land1 = ms_billing_document-landtx.
          ENDIF.

          LOOP AT et_entityset INTO ls_entity.

            SELECT SINGLE text1 FROM t007s INTO ls_entity-taxcodename
                  WHERE mwskz = ls_entity-taxcode AND kalsm = lv_tax_proc AND spras = sy-langu.
            idx = sy-tabix.
            MODIFY et_entityset INDEX idx from ls_entity.
          ENDLOOP.
        SORT et_entityset by conditionratevalue.
        mt_cleared_downpayment = et_entityset.
      ENDIF.
    ENDIF.
  ENDMETHOD.


  METHOD company_get_entity.
    DATA: ls_adrs  TYPE adrs_print,
          ls_adrc  TYPE adrc.
    DATA: lc_country_ch TYPE string VALUE 'CH',
          lc_country_pl TYPE string value 'PL',
          lc_country_in TYPE string value 'IN',
          lc_country_cz TYPE string VALUE 'CZ',
          lc_country_ae TYPE string VALUE 'AE',
          lc_country_om TYPE string VALUE 'OM',
          lc_country_sa TYPE string VALUE 'SA',
          lc_country_eg TYPE string VALUE 'EG'.
    DATA: lv_region_name TYPE bezei.

    DATA :lv_bankn TYPE bankn,
          lv_hbkid TYPE hbkid,
          lv_bankl TYPE bankl.

    CLEAR: ls_adrc,
           lv_region_name.

    TRY.
        super->company_get_entity(
               EXPORTING
                 iv_entity_name          = iv_entity_name
                 iv_entity_set_name      = iv_entity_set_name
                 iv_source_name          = iv_source_name
                 it_key_tab              = it_key_tab
                 io_request_object       = io_request_object
                 io_tech_request_context = io_tech_request_context
                 it_navigation_path      = it_navigation_path
               IMPORTING
                 er_entity               = er_entity
                 es_response_context     = es_response_context ).

        mv_language = get_language( ).
        mv_sender_country = get_sender_country( ).

*        IF mv_sender_country = lc_country_ch or mv_sender_country = lc_country_pl
*          or mv_sender_country = lc_country_in .

          CALL FUNCTION 'ADDRESS_INTO_PRINTFORM'
            EXPORTING
              address_type        = '1'
              address_number      = er_entity-address_id
              receiver_language   = mv_language
              sender_country      = mv_sender_country
              number_of_lines     = 6
              street_has_priority = abap_false
            IMPORTING
              address_printform   = ls_adrs.

** AddressLine1 - AddressLine6
          er_entity-address_line_1 = ls_adrs-line0.
          er_entity-address_line_2 = ls_adrs-line1.
          er_entity-address_line_3 = ls_adrs-line2.
          er_entity-address_line_4 = ls_adrs-line3.
          er_entity-address_line_5 = ls_adrs-line4.
          er_entity-address_line_6 = ls_adrs-line5.

*        ENDIF.

      CATCH /iwbep/cx_mgw_busi_exception .
      CATCH /iwbep/cx_mgw_tech_exception .

    ENDTRY.

    TEST-SEAM fill_er.
    END-TEST-SEAM.

    IF ms_billing_document-landtx = lc_country_in.

      SELECT SINGLE * FROM adrc                  "#EC CI_ALL_FIELDS_NEEDED                    " Fetching region
                      INTO ls_adrc
                       WHERE addrnumber = er_entity-address_id.
      IF sy-subrc = 0.
        SELECT SINGLE bezei FROM t005u                              " Fetching region name
                       INTO  lv_region_name
                       WHERE spras EQ sy-langu AND
                             land1 EQ ls_adrc-country AND
                             bland EQ ls_adrc-region.
        IF sy-subrc = 0.
          er_entity-region_name = lv_region_name.                   " Region Name
          CLEAR: lv_region_name.
        ENDIF.

        er_entity-region = ls_adrc-region.                          " Region
        CLEAR: ls_adrc.
      ENDIF.


    ENDIF.

    IF ms_billing_document-landtx = lc_country_cz OR ms_billing_document-land1 = lc_country_cz.

      SELECT SINGLE hbkid bankl FROM t012
        INTO  (lv_hbkid ,lv_bankl)
        WHERE bukrs = ms_billing_document-bukrs.

      IF sy-subrc = 0.

        SELECT SINGLE bankn FROM t012k
          INTO lv_bankn
          WHERE bukrs = ms_billing_document-bukrs AND hbkid = lv_hbkid.

          IF sy-subrc = 0.
            CONCATENATE lv_bankn lv_bankl INTO er_entity-bank_acc_key SEPARATED BY '/'.
          ENDIF.
      ENDIF.

    ENDIF.
    IF ms_billing_document-landtx = lc_country_ae OR
       ms_billing_document-landtx = lc_country_sa OR
       ms_billing_document-landtx = lc_country_om OR
       ms_billing_document-landtx = lc_country_eg.
      SELECT SINGLE * FROM adrc                                   "#EC CI_ALL_FIELDS_NEEDED
                      INTO ls_adrc
                       WHERE addrnumber = er_entity-address_id. "#EC CI_NOORDER  "#EC CI_ALL_FIELDS_NEEDED
      CONCATENATE ls_adrc-name1 ls_adrc-name2 ls_adrc-name3 ls_adrc-name4 INTO er_entity-full_name
                                                                          SEPARATED BY space.
      CONCATENATE ls_adrc-street ls_adrc-str_suppl1 INTO er_entity-address_line_1 SEPARATED BY space.
      CONCATENATE ls_adrc-str_suppl2 ls_adrc-str_suppl3 INTO er_entity-address_line_2 SEPARATED BY space.
      er_entity-address_line_3 = ls_adrc-house_num1.
      er_entity-address_line_4 = ls_adrc-house_num2.
      er_entity-postal_code = ls_adrc-post_code1.
      er_entity-city = ls_adrc-city1.
      er_entity-countryname = ls_adrc-country.
      er_entity-region         = ls_adrc-region.

      SELECT SINGLE CountryName FROM I_CountryText INTO @DATA(lv_country) WHERE Country = @ls_adrc-country AND Language = @sy-langu.
      er_entity-countryname = lv_country.
      SELECT SINGLE BEZEI FROM T005U INTO er_entity-region_name WHERE SPRAS = 'EN' AND
                                           LAND1 = ms_billing_document-landtx AND
                                           BLAND = ls_adrc-region.
    ENDIF.


  ENDMETHOD.


  METHOD fill_serial_numbers.
    DATA: lt_delivery_vbeln      TYPE TABLE OF vbeln_vl,
          lt_salesorder_vbeln    TYPE TABLE OF vbeln_vauf,
          lt_xvbrp               TYPE STANDARD TABLE OF vbrpvb,
          ls_item_salesorder_ref LIKE LINE OF mt_item_salesorder_ref,
          ls_item_delivery_ref   LIKE LINE OF mt_item_delivery_ref,
          ls_serial_number       LIKE LINE OF mt_serial_numbers,
          lv_fill_so             TYPE abap_bool,
          lv_fill_delivery       TYPE abap_bool,
          lo_data_buffer         TYPE REF TO cl_fdp_v3_data_buffer.

    DATA: ls_rserob TYPE rserob,
          lt_sernos TYPE rserob_t.

    FIELD-SYMBOLS: <fs_item>             TYPE vbdpr,
                   <fs_vbrp>             TYPE vbrpvb,
                   <fs_delivery_vbeln>   TYPE vbeln_vl,
                   <fs_salesorder_vbeln> TYPE vbeln_vauf.

    lo_data_buffer = cl_fdp_v3_bd_form_utility=>get_data_buffer( ).


* find all preceeding documents (best would be delivery, but if this is not available take sales order)
    LOOP AT lo_data_buffer->mt_item ASSIGNING <fs_item>.
      IF <fs_item>-vbeln_vl IS NOT INITIAL.
        INSERT <fs_item>-vbeln_vl INTO TABLE lt_delivery_vbeln.
      ELSE.
        IF <fs_item>-vbeln_vauf IS NOT INITIAL.
          INSERT <fs_item>-vbeln_vauf INTO TABLE lt_salesorder_vbeln.
        ENDIF.
      ENDIF.
    ENDLOOP.
    DELETE ADJACENT DUPLICATES FROM lt_delivery_vbeln.
    DELETE ADJACENT DUPLICATES FROM lt_salesorder_vbeln.

* first get serial numbers from delivery

    LOOP AT lt_delivery_vbeln ASSIGNING <fs_delivery_vbeln>.
      CLEAR: ls_rserob, lt_sernos.
      ls_rserob-taser = 'SER01'.
      ls_rserob-lief_nr = <fs_delivery_vbeln>.

      CALL FUNCTION 'GET_SERNOS_OF_DOCUMENT'
        EXPORTING
          key_data            = ls_rserob
          status_pre_read     = ' '
        TABLES
          sernos              = lt_sernos
        EXCEPTIONS
          key_parameter_error = 1
          no_supported_access = 2
          no_data_found       = 3
          OTHERS              = 4.

      INSERT LINES OF lt_sernos INTO TABLE mt_serial_numbers.
    ENDLOOP.
* then get serial numbers from sales orders

    LOOP AT lt_salesorder_vbeln ASSIGNING <fs_salesorder_vbeln>.
      CLEAR: ls_rserob, lt_sernos.

      ls_rserob-taser = 'SER02'.
      ls_rserob-sdaufnr = <fs_salesorder_vbeln>.

      CALL FUNCTION 'GET_SERNOS_OF_DOCUMENT'
        EXPORTING
          key_data            = ls_rserob
          status_pre_read     = ' '
        TABLES
          sernos              = lt_sernos
        EXCEPTIONS
          key_parameter_error = 1
          no_supported_access = 2
          no_data_found       = 3
          OTHERS              = 4.

      INSERT LINES OF lt_sernos INTO TABLE mt_serial_numbers.
    ENDLOOP.

* to make sure this coding is not called several times if no serial numbers involved fill dummy line in mt_serial_numbers
    IF mt_serial_numbers IS INITIAL.
      ls_serial_number-lief_nr = '0'.
      ls_serial_number-sdaufnr = '0'.
      INSERT ls_serial_number INTO TABLE mt_serial_numbers.
    ENDIF.

  ENDMETHOD.


  METHOD invoiceitemset_get_entityset.
    DATA: lc_country_se TYPE string VALUE 'SE',
          lc_country_it TYPE string VALUE 'IT',
          lc_country_fi TYPE string VALUE 'FI',
          lc_country_no TYPE string VALUE 'NO',
          lc_country_pl TYPE string VALUE 'PL',
          lc_country_br TYPE string VALUE 'BR',
          lc_country_in TYPE string VALUE 'IN',
          lc_country_cz TYPE string VALUE 'CZ',
          lc_country_ae TYPE string VALUE 'AE',
          lc_country_om TYPE string VALUE 'OM',
          lc_country_be TYPE string VALUE 'BE',
          lc_country_sa TYPE string VALUE 'SA',
          lc_country_eg TYPE string VALUE 'EG'.

* Declaration for Country Brazil
    DATA: lt_komv  TYPE komv_tab.
    DATA: lo_data_buffer TYPE REF TO cl_fdp_v3_data_buffer.
    lo_data_buffer = cl_fdp_v3_bd_form_utility=>get_data_buffer( ).

* Declarations for Country Sweden
    DATA:  lv_vbeln TYPE vbrk-vbeln.

* Declarations for Country Italy
    TYPES : BEGIN OF ty_refdelivery,
              posnr TYPE posnr,
              vbeln TYPE vbeln_vl,
              xabln TYPE xabln,
            END OF ty_refdelivery.
    DATA: ls_entityset TYPE cl_fdp_v3_bd_standard_mpc=>ts_billingdocumentitemnode,
          lt_entityset TYPE cl_fdp_v3_bd_standard_mpc=>tt_billingdocumentitemnode.
    DATA : ls_refdelivery TYPE ty_refdelivery.
    DATA : lt_refdelivery TYPE STANDARD TABLE OF ty_refdelivery.


    TYPES : BEGIN OF ty_returns,
              vbeln TYPE vbeln_vf,
              posnr TYPE posnr_vf,
              shkzg TYPE shkzg_vf,
              vgpos TYPE vgpos,
            END OF ty_returns,

            BEGIN OF ty_prcd_elements,
              kposn TYPE kposn,
              kbetr TYPE kbetr,
            END OF ty_prcd_elements,

           BEGIN OF ty_prcd_elements1,
              kposn TYPE kposn,
              kschl TYPE kschl,
              kbetr TYPE kbetr,
              kwert TYPE kwert,
              kpein TYPE kpein,
              kstat TYPE kstat,
              kinak TYPE kinak,
              kntyp TYPE kntyp,
              koaid TYPE koaid,
            END OF ty_prcd_elements1.
    TYPES:  BEGIN OF ty_value_mapping,
              vmapname(20),
              ext_value(200),
              int_value(200),
            END OF ty_value_mapping .

    DATA: ls_returns               TYPE ty_returns,
          lt_returns               TYPE TABLE OF ty_returns,
          lt_item_price_conditions TYPE cl_fdp_v3_bd_form_utility=>tt_price_conditions,
          lt_prcd_elements         TYPE TABLE OF ty_prcd_elements,
          lt_prcd_elements1        TYPE TABLE OF ty_prcd_elements1,
          lt_prcd_elements2 TYPE TABLE OF ty_prcd_elements1,
          lt_prcd_elements3 TYPE TABLE OF ty_prcd_elements1,
          lv_local_amount  TYPE kwert,
          lv_exchange_rate TYPE string,
          lc_curr TYPE waerl.
    DATA : lt_surcharge_eg TYPE TABLE OF ty_prcd_elements1,
           ls_surcharge_eg TYPE ty_prcd_elements1.
    DATA : lt_value_mapping TYPE TABLE OF ty_value_mapping,
           ls_value_mapping TYPE ty_value_mapping,
           lv_surcharge TYPE P LENGTH 16 DECIMALS 5.
    CONSTANTS : lc_vmap_val_master TYPE char15 VALUE '/AIF/T_MVMAPVAL'.
    FIELD-SYMBOLS: <fs_tab_entityset>      LIKE LINE OF et_entityset,
                   <fs_tab_entityset1>     LIKE LINE OF et_entityset,
                   <fs_tab_prcd_elements>  TYPE ty_prcd_elements,
                   <fs_tab_prcd_elements1> TYPE ty_prcd_elements1.

    CLEAR :ls_returns,
           lt_returns,
           ls_entityset,
           lt_prcd_elements,
           lt_prcd_elements1,
           lt_item_price_conditions.

    REFRESH :lt_returns,
             lt_prcd_elements,
             lt_prcd_elements1,
             lt_item_price_conditions.

* Declarations for country India
    TYPES: BEGIN OF ty_vbrp,
             vbeln TYPE vbeln_vf,
             posnr TYPE posnr_vf,
             matnr TYPE matnr,
             werks TYPE werks_d,
           END OF ty_vbrp.

    DATA: ls_vbrp TYPE ty_vbrp,
          lt_vbrp TYPE TABLE OF ty_vbrp.
* Declaration For SA,AE and EG
    TYPES: BEGIN OF ty_vbrp_ar,
             vbeln TYPE vbeln_vf,
             posnr TYPE posnr_vf,
             netwr TYPE netwr,
             mwsbp TYPE mwsbp,
             arktx TYPE arktx,
           END OF ty_vbrp_ar.
    DATA: ls_vbrp_ar TYPE ty_vbrp_ar,
          lt_vbrp_ar TYPE TABLE OF ty_vbrp_ar.

    TEST-SEAM skip_get.
    TRY.
        CALL METHOD super->invoiceitemset_get_entityset
          EXPORTING
            iv_entity_name           = iv_entity_name
            iv_entity_set_name       = iv_entity_set_name
            iv_source_name           = iv_source_name
            it_filter_select_options = it_filter_select_options
            is_paging                = is_paging
            it_key_tab               = it_key_tab
            it_navigation_path       = it_navigation_path
            it_order                 = it_order
            iv_filter_string         = iv_filter_string
            iv_search_string         = iv_search_string
            io_tech_request_context  = io_tech_request_context
          IMPORTING
            et_entityset             = et_entityset
            es_response_context      = es_response_context.
      CATCH /iwbep/cx_mgw_busi_exception .
      CATCH /iwbep/cx_mgw_tech_exception .
    ENDTRY.
    END-TEST-SEAM.

    IF ms_billing_document-landtx = lc_country_se OR
       ms_billing_document-landtx = lc_country_fi OR
       ms_billing_document-landtx = lc_country_no OR
       ms_billing_document-landtx = lc_country_pl OR
       ms_billing_document-landtx = lc_country_be.
* Get BillingDocument to identify the tax code.
      lv_vbeln = me->get_billing_document( ).
      IF lv_vbeln IS NOT INITIAL.
        CALL METHOD cl_glo_log_form_utility=>get_billingitem
          EXPORTING
            ev_billingdocument = lv_vbeln
          CHANGING
            ct_billingitem     = et_entityset.
      ENDIF.
    ENDIF.

    TEST-SEAM fill_et.
    END-TEST-SEAM.

    IF ms_billing_document-landtx = lc_country_it.
*  Getting the Goods Reciept/Issue slip Number based on the delivery document for Italy

      IF et_entityset IS NOT INITIAL.
        REFRESH lt_refdelivery.
        CLEAR: ls_entityset,
             ls_refdelivery.

        LOOP AT et_entityset INTO ls_entityset.
          IF ls_entityset-reference_sd_document_category EQ 'J'.
            ls_refdelivery-posnr = ls_entityset-billing_document_item.
            ls_refdelivery-vbeln = ls_entityset-reference_sd_document.
            APPEND ls_refdelivery TO lt_refdelivery.
            CLEAR ls_refdelivery.
          ENDIF.
          CLEAR ls_entityset.
        ENDLOOP.

        IF lt_refdelivery IS NOT INITIAL.
          CALL METHOD cl_glo_log_form_utility=>get_reference_slip_number
            CHANGING
              ct_referencedelivery = lt_refdelivery.
          IF sy-subrc = 0.
            LOOP AT et_entityset INTO ls_entityset.
              READ TABLE lt_refdelivery INTO ls_refdelivery WITH KEY posnr = ls_entityset-billing_document_item.
              IF sy-subrc = 0.
                ls_entityset-reference_slip_number = ls_refdelivery-xabln.
                MODIFY et_entityset FROM ls_entityset INDEX sy-tabix TRANSPORTING reference_slip_number .
              ENDIF.
              CLEAR: ls_refdelivery,
                     ls_entityset.
            ENDLOOP.

          ENDIF.
        ENDIF.

      ENDIF.
    ENDIF.

*** Poland :  Invoice Forms
    IF ms_billing_document-landtx = lc_country_pl OR ms_billing_document-landtx = lc_country_cz.

*** To Fetch Tax rate
      SELECT kposn kbetr FROM prcd_elements INTO TABLE lt_prcd_elements FOR ALL ENTRIES IN et_entityset WHERE knumv = ms_billing_document-knumv AND
                                                                                kposn = et_entityset-billing_document_item AND
                                                                                  kappl = 'V'  AND
                                                                                  koaid = 'D' AND
                                                                                  kntyp = 'D' AND
                                                                                  kinak = ' ' AND
                                                                                  kstat = ' '.
    ENDIF.

    IF ms_billing_document-landtx = lc_country_pl.
***  To fetch the return field and reference sd document item for the line items
      SELECT * FROM vbrp
                    INTO CORRESPONDING FIELDS OF TABLE lt_returns
                    FOR ALL ENTRIES IN et_entityset
                    WHERE vbeln = et_entityset-billing_document
                    AND posnr = et_entityset-billing_document_item.


      IF lt_prcd_elements IS NOT INITIAL.
        LOOP AT et_entityset ASSIGNING <fs_tab_entityset>.

          CASE <fs_tab_entityset>-tax_code.

            WHEN 'A0' OR 'A8' OR 'A9'.
              <fs_tab_entityset>-tax_rate = 'zw'.

            WHEN 'A5' OR 'C3' OR 'C4'.
              <fs_tab_entityset>-tax_rate = 'np'.

            WHEN 'A6' OR 'A7'.
              <fs_tab_entityset>-tax_rate = 'oo'.

            WHEN OTHERS.

              READ TABLE lt_prcd_elements WITH TABLE KEY kposn = <fs_tab_entityset>-billing_document_item ASSIGNING <fs_tab_prcd_elements>.
              IF sy-subrc = 0.
                <fs_tab_entityset>-tax_rate = <fs_tab_prcd_elements>-kbetr.

                CONDENSE <fs_tab_entityset>-tax_rate.
              ENDIF.
          ENDCASE.


          IF ms_billing_document-vbtyp NE 'M'.             " Correction Invoice


            READ TABLE lt_returns INTO ls_returns WITH KEY vbeln = <fs_tab_entityset>-billing_document
                                                           posnr = <fs_tab_entityset>-billing_document_item.

            IF sy-subrc = 0.

              <fs_tab_entityset>-returns = ls_returns-shkzg.                      "Returns field
              <fs_tab_entityset>-reference_sd_document_item = ls_returns-vgpos.   "Reference SD Document Item

            ENDIF.


*** Item Net Price & Buffer Item Price Conditions to avoid additional call in Item Price Components Entity
            cl_fdp_v3_bd_form_utility=>get_price_conditions_item(
              EXPORTING
                is_billing_document            = ms_billing_document
                iv_billing_document_item       = <fs_tab_entityset>-billing_document_item
                iv_language                    = mv_language
                iv_item_quantity               = <fs_tab_entityset>-quantity
                iv_item_quantity_unit          = <fs_tab_entityset>-quantity_internal_unit
                iv_exchange_rate               = <fs_tab_entityset>-exchange_rate
                iv_exchange_rate_date          = <fs_tab_entityset>-exchange_rate_date
                iv_return_item_proc_code       = <fs_tab_entityset>-return_item_proc_type
              IMPORTING
                et_price_conditions            = lt_item_price_conditions
                ev_net_price                   = <fs_tab_entityset>-net_price
                ev_net_price_quantity          = <fs_tab_entityset>-net_price_quantity
                ev_net_price_qnt_internal_unit = <fs_tab_entityset>-net_price_qnt_internal_unit
                ev_net_price_qnt_ut_tech_name  = <fs_tab_entityset>-net_price_qnt_unit_tech_name
            ).

            INSERT LINES OF lt_item_price_conditions
                   INTO TABLE mt_item_price_conditions.

            CLEAR: ls_returns,
                   lt_item_price_conditions.
            REFRESH : lt_item_price_conditions.

          ENDIF.
        ENDLOOP.
      ENDIF.

      IF  ms_billing_document-vbtyp NE 'M' AND             " Correction Invoice
          mv_correction_indicator NE 'X'.                  " Credit/Debit Based ; Not Differential

*** Get after correction and corresponding difference entries
        CALL METHOD cl_glo_log_form_utility=>get_correction_difference
          EXPORTING
            it_item_pricing_condition  = mt_item_price_conditions
            iv_vbtyp                   = ms_billing_document-vbtyp
          IMPORTING
            et_item_difference         = mt_item_difference
            et_item_pricing_difference = mt_item_pricing_difference
            et_item_aftcorr            = mt_item_after_correction
            et_item_pricing_aftcorr    = mt_item_pricing_aftercorr
          CHANGING
            ct_item                    = et_entityset.

      ENDIF.
    ENDIF.

    " Brazil:
    " it is necessary to get the items IBRX as net amount
    " net price will be: net amount / quantity
    IF lo_data_buffer->ms_header-lland = lc_country_br AND ms_billing_document-landtx = lc_country_br.

      DATA lo_billing_output_mngmt TYPE REF TO cl_j1b_billing_output_mngmt.
      CREATE OBJECT lo_billing_output_mngmt.

      CALL METHOD cl_fdp_v3_bd_trans_data_helper=>get_transient_data "get pricing data
        IMPORTING
          et_komv = lt_komv.

      lo_billing_output_mngmt->if_j1b_billing_output_mngmt~get_invoice_item_set_entity(
        EXPORTING
          iv_country      = lo_data_buffer->ms_header-lland    " Country Key
          it_pricing_data = lt_komv                            " Table type komv
        CHANGING
          ct_entityset    = et_entityset
      ).

    ENDIF.

*** India
    IF ms_billing_document-landtx = lc_country_in.

      CLEAR: ls_vbrp,
             lt_vbrp.

      SELECT vbeln posnr matnr werks FROM vbrp                              "Fetching Plant Information
             INTO CORRESPONDING FIELDS OF TABLE lt_vbrp
             FOR ALL ENTRIES IN et_entityset
             WHERE vbeln = et_entityset-billing_document
             AND   posnr = et_entityset-billing_document_item.

      IF lt_vbrp IS NOT INITIAL.

        LOOP AT et_entityset ASSIGNING <fs_tab_entityset>.
          READ TABLE lt_vbrp INTO ls_vbrp WITH KEY vbeln = <fs_tab_entityset>-billing_document
                                                   posnr = <fs_tab_entityset>-billing_document_item.
          IF sy-subrc = 0.
            <fs_tab_entityset>-plant = ls_vbrp-werks.      " Moving plant details to corresponding items
          ENDIF.
          CLEAR: ls_vbrp.
        ENDLOOP.

        CALL METHOD cl_glo_log_form_utility=>get_hsn_sac_code   "Fetching HSN/SAC Code Details
          EXPORTING
            iv_spras = sy-langu
            iv_land1 = 'IN'
          CHANGING
            ct_items = et_entityset.

      ENDIF.

    ENDIF.
****CZ : invoice forms
    IF ms_billing_document-landtx = lc_country_cz.
      LOOP AT et_entityset ASSIGNING <fs_tab_entityset>.
        IF <fs_tab_entityset>-total_amount IS INITIAL.
          IF <fs_tab_entityset>-tax_amount IS NOT INITIAL AND <fs_tab_entityset>-net_amount IS NOT INITIAL.
            <fs_tab_entityset>-total_amount = <fs_tab_entityset>-net_amount + <fs_tab_entityset>-tax_amount.
          ELSE.
            <fs_tab_entityset>-total_amount = <fs_tab_entityset>-net_amount.
          ENDIF.
        ENDIF.
        READ TABLE lt_prcd_elements WITH TABLE KEY kposn = <fs_tab_entityset>-billing_document_item ASSIGNING <fs_tab_prcd_elements>.
        IF sy-subrc = 0.
          <fs_tab_entityset>-tax_rate = <fs_tab_prcd_elements>-kbetr.
          CONDENSE <fs_tab_entityset>-tax_rate.
        ENDIF.
      ENDLOOP.
    ENDIF.

    "1908 HFC02 changes for KSA/UAE Customer Invoice Forms for Unit Price and VAT Rate
    IF ms_billing_document-landtx = lc_country_ae OR
       ms_billing_document-landtx = lc_country_sa OR
       ms_billing_document-landtx = lc_country_om OR
       ms_billing_document-landtx = lc_country_eg.
      IF NOT et_entityset IS INITIAL.
       IF ms_billing_document-landtx EQ 'EG'.
         lc_curr = 'EGP'.
         SELECT vmapname int_value ext_value FROM (lc_vmap_val_master)
                INTO CORRESPONDING FIELDS OF TABLE lt_value_mapping
                WHERE ns = '/EDOEG'  AND vmapname = 'CONDITION_TYPES'.
       ELSEIF ms_billing_document-landtx EQ 'AE'.
         lc_curr = 'AED'.
       ELSEIF ms_billing_document-landtx EQ 'OM'.
         lc_curr = 'OMR'.
       ELSEIF ms_billing_document-landtx EQ 'SA'.
         lc_curr = 'SAR'.
      ENDIF.
      SELECT vbeln posnr netwr mwsbp arktx FROM vbrp INTO CORRESPONDING FIELDS OF TABLE lt_vbrp_ar
                                                     FOR ALL ENTRIES IN et_entityset
                                                     WHERE vbeln = et_entityset-billing_document
                                                     AND posnr = et_entityset-billing_document_item.

      SELECT kposn kschl kbetr kwert kpein kstat kinak kntyp koaid FROM prcd_elements INTO TABLE lt_prcd_elements1 FOR ALL ENTRIES IN et_entityset
       WHERE knumv = ms_billing_document-knumv AND
             kposn = et_entityset-billing_document_item AND
             koaid IN ('B','D','A').
      UNASSIGN <fs_tab_prcd_elements1>.
      LOOP AT lt_prcd_elements1 ASSIGNING <fs_tab_prcd_elements1>.
        IF <fs_tab_prcd_elements1>-kstat = '' AND <fs_tab_prcd_elements1>-kinak = '' AND
           <fs_tab_prcd_elements1>-kntyp = '' AND <fs_tab_prcd_elements1>-koaid = 'A' AND <fs_tab_prcd_elements1>-kwert LT '0'.
           COLLECT <fs_tab_prcd_elements1> INTO lt_prcd_elements2.
        ELSEIF <fs_tab_prcd_elements1>-kstat = '' AND <fs_tab_prcd_elements1>-kinak = '' AND
           <fs_tab_prcd_elements1>-kwert GT '0' AND <fs_tab_prcd_elements1>-koaid = 'A'.
           IF ms_billing_document-landtx EQ 'EG'.
             READ TABLE lt_value_mapping INTO ls_value_mapping WITH KEY ext_value = <fs_tab_prcd_elements1>-kschl.
              IF sy-subrc = 0.
               CLEAR <fs_tab_prcd_elements1>-kntyp.
               COLLECT <fs_tab_prcd_elements1> INTO lt_prcd_elements3.
              ELSE.
               CLEAR <fs_tab_prcd_elements1>-kntyp.
               COLLECT <fs_tab_prcd_elements1> INTO lt_surcharge_eg.
              ENDIF.
           ELSE.
              CLEAR <fs_tab_prcd_elements1>-kntyp.
              COLLECT <fs_tab_prcd_elements1> INTO lt_prcd_elements3.
           ENDIF.
        ENDIF.
      ENDLOOP.

      TEST-SEAM TS_2. END-TEST-SEAM.
      IF sy-subrc = 0.
        DELETE lt_prcd_elements1 WHERE kstat = 'X' AND kinak = 'Y'.
        SORT lt_prcd_elements1 BY kposn kntyp koaid.
        SORT lt_prcd_elements2 BY kposn kntyp koaid.
        SORT lt_prcd_elements3 BY kposn kntyp koaid.
        SORT lt_surcharge_eg   BY kposn kntyp koaid.
        LOOP AT et_entityset ASSIGNING <fs_tab_entityset1>.
          READ TABLE lt_vbrp_ar INTO ls_vbrp_ar WITH KEY vbeln = <fs_tab_entityset1>-billing_document
                                                   posnr = <fs_tab_entityset1>-billing_document_item.
          "Tax Amount
          <fs_tab_entityset1>-tax_amount = ls_vbrp_ar-mwsbp.
          "Total Amount
          <fs_tab_entityset1>-total_amount = <fs_tab_entityset1>-net_amount + ls_vbrp_ar-mwsbp.
          "IF NOT lt_prcd_elements1 IS INITIAL.
          UNASSIGN <fs_tab_prcd_elements1>.
          READ TABLE lt_prcd_elements1 WITH KEY kposn = <fs_tab_entityset1>-billing_document_item
           kntyp = ' ' koaid = 'B' ASSIGNING <fs_tab_prcd_elements1> BINARY SEARCH.
          IF sy-subrc = 0.
            <fs_tab_entityset1>-unitprice = <fs_tab_prcd_elements1>-kwert / <fs_tab_entityset1>-quantity .
          ENDIF.
          IF ms_billing_document-landtx EQ 'EG' AND lt_surcharge_eg IS NOT INITIAL.
           READ TABLE lt_surcharge_eg WITH KEY kposn = <fs_tab_entityset1>-billing_document_item
           koaid = 'A' INTO ls_surcharge_eg BINARY SEARCH.
           IF sy-subrc = 0.
            IF ls_surcharge_eg-kwert GT 0.
              <fs_tab_entityset1>-unitprice = <fs_tab_entityset1>-unitprice +
                                        ( ls_surcharge_eg-kwert / <fs_tab_entityset1>-quantity ).
            ENDIF.
           ENDIF.
          ENDIF.
          UNASSIGN <fs_tab_prcd_elements1>.
          READ TABLE lt_prcd_elements1 WITH KEY kposn = <fs_tab_entityset1>-billing_document_item
           kntyp = 'D' koaid = 'D' ASSIGNING <fs_tab_prcd_elements1> BINARY SEARCH.
          IF sy-subrc = 0.
            <fs_tab_entityset1>-tax_rate = <fs_tab_prcd_elements1>-kbetr.
            CONDENSE <fs_tab_entityset1>-tax_rate.
          ENDIF.

          UNASSIGN <fs_tab_prcd_elements1>.
          READ TABLE lt_prcd_elements2 WITH KEY kposn = <fs_tab_entityset1>-billing_document_item
          kntyp = '' koaid = 'A' ASSIGNING <fs_tab_prcd_elements1> BINARY SEARCH.
          IF sy-subrc = 0.
            "Discount Amount
            IF <fs_tab_prcd_elements1>-kwert LT 0.
              <fs_tab_entityset1>-item_discount = -1 * <fs_tab_prcd_elements1>-kwert.
            ENDIF.
          ENDIF.
          UNASSIGN <fs_tab_prcd_elements1>.
          READ TABLE lt_prcd_elements3 WITH KEY kposn = <fs_tab_entityset1>-billing_document_item
          koaid = 'A' ASSIGNING <fs_tab_prcd_elements1> BINARY SEARCH.
          IF sy-subrc = 0.
            "Other Charges
            IF <fs_tab_prcd_elements1>-kwert GT 0.
              <fs_tab_entityset1>-other_charges =  <fs_tab_prcd_elements1>-kwert.
            ENDIF.
          ENDIF.
          clear ls_vbrp_ar.
         "Convert to local Currency
         IF <fs_tab_entityset1>-currency NE lc_curr.
           IF <fs_tab_entityset1>-net_amount IS NOT INITIAL.
              CALL FUNCTION 'CONVERT_TO_LOCAL_CURRENCY'
                EXPORTING
                  date             =  ms_billing_document-fkdat
                  foreign_amount   = <fs_tab_entityset1>-net_amount
                  foreign_currency = <fs_tab_entityset1>-currency
                  local_currency   = lc_curr
                IMPORTING
                  exchange_rate    = lv_exchange_rate
                  local_amount     = lv_local_amount
                EXCEPTIONS
                  no_rate_found    = 1
                  overflow         = 2
                  no_factors_found = 3
                  no_spread_found  = 4
                  derived_2_times  = 5
                  OTHERS           = 6.
               IF sy-subrc <> 0.
*       Implement suitable error handling here
               ENDIF.
               <fs_tab_entityset1>-net_amount_loccurr = lv_local_amount.
               CLEAR: lv_local_amount, lv_exchange_rate.
              ENDIF.
              IF <fs_tab_entityset1>-tax_amount IS NOT INITIAL.
              CALL FUNCTION 'CONVERT_TO_LOCAL_CURRENCY'
                EXPORTING
                  date             =  ms_billing_document-fkdat
                  foreign_amount   = <fs_tab_entityset1>-tax_amount
                  foreign_currency = <fs_tab_entityset1>-currency
                  local_currency   = lc_curr
                IMPORTING
                  exchange_rate    = lv_exchange_rate
                  local_amount     = lv_local_amount
                EXCEPTIONS
                  no_rate_found    = 1
                  overflow         = 2
                  no_factors_found = 3
                  no_spread_found  = 4
                  derived_2_times  = 5
                  OTHERS           = 6.
               IF sy-subrc <> 0.
*       Implement suitable error handling here
               ENDIF.
               <fs_tab_entityset1>-tax_amount_loccurr = lv_local_amount.
               CLEAR: lv_local_amount, lv_exchange_rate.
              ENDIF.
              IF <fs_tab_entityset1>-total_amount IS NOT INITIAL.
              CALL FUNCTION 'CONVERT_TO_LOCAL_CURRENCY'
                EXPORTING
                  date             =  ms_billing_document-fkdat
                  foreign_amount   = <fs_tab_entityset1>-total_amount
                  foreign_currency = <fs_tab_entityset1>-currency
                  local_currency   = lc_curr
                IMPORTING
                  exchange_rate    = lv_exchange_rate
                  local_amount     = lv_local_amount
                EXCEPTIONS
                  no_rate_found    = 1
                  overflow         = 2
                  no_factors_found = 3
                  no_spread_found  = 4
                  derived_2_times  = 5
                  OTHERS           = 6.
               IF sy-subrc <> 0.
*       Implement suitable error handling here
               ENDIF.
               <fs_tab_entityset1>-total_amount_loccurr = lv_local_amount.
               CLEAR: lv_local_amount, lv_exchange_rate.
              ENDIF.
              ELSE.
                <fs_tab_entityset1>-tax_amount_loccurr = <fs_tab_entityset1>-tax_amount.
                <fs_tab_entityset1>-net_amount_loccurr = <fs_tab_entityset1>-net_amount.
                <fs_tab_entityset1>-total_amount_loccurr = <fs_tab_entityset1>-total_amount.
            ENDIF.
        ENDLOOP.
      ENDIF.
      ENDIF.
    ENDIF.
    "1908 HFC02 for United Arab Emirates Customer Invoice Form
    IF ms_billing_document-landtx = lc_country_ae.
      CLEAR: ls_vbrp,
       lt_vbrp.

      SELECT vbeln posnr matnr werks FROM vbrp                              "Fetching Plant Information
       INTO CORRESPONDING FIELDS OF TABLE lt_vbrp
       FOR ALL ENTRIES IN et_entityset
       WHERE vbeln = et_entityset-billing_document
       AND   posnr = et_entityset-billing_document_item.

      IF lt_vbrp IS NOT INITIAL.

        LOOP AT et_entityset ASSIGNING <fs_tab_entityset>.
          READ TABLE lt_vbrp INTO ls_vbrp WITH KEY vbeln = <fs_tab_entityset>-billing_document
                                              posnr = <fs_tab_entityset>-billing_document_item.
          IF sy-subrc = 0.
            <fs_tab_entityset>-plant = ls_vbrp-werks.      " Moving plant details to corresponding items
          ENDIF.
          CLEAR: ls_vbrp.
        ENDLOOP.
        CALL METHOD cl_glo_log_form_utility=>get_hsn_sac_code   "Fetching HSN/SAC Code Details
          EXPORTING
            iv_spras = sy-langu
            iv_land1 = 'AE'
          CHANGING
            ct_items = et_entityset.
        CALL METHOD cl_glo_log_form_utility=>get_hsn_sac_code   "Fetching HSN/SAC Code Details
          EXPORTING
            iv_spras = sy-langu
            iv_land1 = 'OM'
          CHANGING
            ct_items = et_entityset.
      ENDIF.
    ENDIF.
    "1908 HFC02 for Saudi Arabia Customer Invoice Form
    IF ms_billing_document-landtx = lc_country_sa.
      CLEAR: ls_vbrp,
       lt_vbrp.

      SELECT vbeln posnr matnr werks FROM vbrp                              "Fetching Plant Information
       INTO CORRESPONDING FIELDS OF TABLE lt_vbrp
       FOR ALL ENTRIES IN et_entityset
       WHERE vbeln = et_entityset-billing_document
       AND   posnr = et_entityset-billing_document_item.

      IF lt_vbrp IS NOT INITIAL.

        LOOP AT et_entityset ASSIGNING <fs_tab_entityset>.
          READ TABLE lt_vbrp INTO ls_vbrp WITH KEY vbeln = <fs_tab_entityset>-billing_document
                                              posnr = <fs_tab_entityset>-billing_document_item.
          IF sy-subrc = 0.
            <fs_tab_entityset>-plant = ls_vbrp-werks.      " Moving plant details to corresponding items
          ENDIF.
          CLEAR: ls_vbrp.
        ENDLOOP.
        CALL METHOD cl_glo_log_form_utility=>get_hsn_sac_code   "Fetching HSN/SAC Code Details
          EXPORTING
            iv_spras = sy-langu
            iv_land1 = 'SA'
          CHANGING
            ct_items = et_entityset.
      ENDIF.
    ENDIF.
    "Egypt
    IF ms_billing_document-landtx = lc_country_eg.
      CLEAR: ls_vbrp,
       lt_vbrp.

      SELECT vbeln posnr matnr werks FROM vbrp                              "Fetching Plant Information
       INTO CORRESPONDING FIELDS OF TABLE lt_vbrp
       FOR ALL ENTRIES IN et_entityset
       WHERE vbeln = et_entityset-billing_document
       AND   posnr = et_entityset-billing_document_item.

      IF lt_vbrp IS NOT INITIAL.

        LOOP AT et_entityset ASSIGNING <fs_tab_entityset>.
          READ TABLE lt_vbrp INTO ls_vbrp WITH KEY vbeln = <fs_tab_entityset>-billing_document
                                              posnr = <fs_tab_entityset>-billing_document_item.
          IF sy-subrc = 0.
            <fs_tab_entityset>-plant = ls_vbrp-werks.      " Moving plant details to corresponding items
          ENDIF.
          CLEAR: ls_vbrp.
        ENDLOOP.
        CALL METHOD cl_glo_log_form_utility=>get_hsn_sac_code   "Fetching HSN/SAC Code Details
          EXPORTING
            iv_spras = sy-langu
            iv_land1 = 'EG'
          CHANGING
            ct_items = et_entityset.
      ENDIF.
    ENDIF.
*mt_billing_document_item = et_entityset.
  ENDMETHOD.


  METHOD invoiceset_get_entity.
    DATA: lc_country_hu TYPE string VALUE 'HU',
          lc_country_be TYPE string VALUE 'BE',
          lc_country_lu TYPE string VALUE 'LU',
          lc_country_it TYPE string VALUE 'IT',
          lc_country_es TYPE string VALUE 'ES',
          lc_country_se TYPE string VALUE 'SE',
          lc_country_id TYPE string VALUE 'ID',
          lc_country_no TYPE string VALUE 'NO',
          lc_country_pl TYPE string VALUE 'PL',
          lc_country_fi TYPE string VALUE 'FI',
          lc_lcit       TYPE string VALUE 'LCIT',
          lc_curr_th    TYPE string VALUE 'SATANG',
          lc_curr_ae    TYPE string VALUE 'FILS',      "1908 HFC02 - UAE Customer Invoice Forms
          lc_curr_om    TYPE string VALUE 'BAISAS',
          lc_curr_sa    TYPE string VALUE 'HALALAS',   "1908 HFC02 - UAE Customer Invoice Forms
          lc_country_br TYPE string VALUE 'BR',
          lc_country_at TYPE string VALUE 'AT',
          lc_country_in TYPE string VALUE 'IN',
          lc_country_th TYPE string VALUE 'TH',
          lc_country_cz TYPE string VALUE 'CZ',
          lc_country_ae TYPE string VALUE 'AE',
          lc_country_om TYPE string VALUE 'OM',
          lc_country_sa TYPE string VALUE 'SA',
          lc_country_gb TYPE string VALUE 'GB',
          lc_country_ro TYPE string VALUE 'RO',
          lc_country_eg TYPE string VALUE 'EG',
          lc_curr_eg    TYPE string VALUE 'QIRSH',
          lo_curr_ae    TYPE string VALUE 'فلس',
          lo_curr_om    TYPE string VALUE 'بيسة',
          lo_curr_sa    TYPE string VALUE 'هللة',
          lo_curr_eg    TYPE string VALUE 'قرش'.

* Declarations for Country Brazil
    DATA: lt_komv  TYPE komv_tab.
    DATA lt_pricecondition TYPE cl_fdp_v3_bd_standard_mpc=>tt_pricingconditionnode.
    DATA lt_filter_select_options TYPE /iwbep/t_mgw_select_option.
    DATA lt_order TYPE /iwbep/t_mgw_sorting_order.
    DATA ls_paging TYPE /iwbep/s_mgw_paging.
    DATA lv_filter_string	TYPE string.
    DATA lv_search_string	TYPE string.
    DATA: lo_data_buffer TYPE REF TO cl_fdp_v3_data_buffer.
    lo_data_buffer = cl_fdp_v3_bd_form_utility=>get_data_buffer( ).

    TYPES : BEGIN OF ty_refdelivery,
              posnr TYPE posnr,
              vbeln TYPE vbeln_vl,
              xabln TYPE xabln,
            END OF ty_refdelivery.

    DATA: lv_compcode   TYPE bukrs,
          lv_fiscalyear TYPE gjahr,
          lv_vatdate    TYPE vatdate.

    DATA : ls_refdelivery TYPE ty_refdelivery.
    DATA : lt_refdelivery TYPE STANDARD TABLE OF ty_refdelivery.

    DATA : lv_words TYPE char255,
           lt_words TYPE spell,
           lv_ktext TYPE ktext_curt,
           lv_fkdat TYPE fkdat,
           lv_augru TYPE augru,
           lv_bezei TYPE bezei40,
           lv_auart TYPE auart,
           lv_vbklt TYPE vbklt,
           lv_vbeln TYPE vbeln_vf,
           lv_vgbel TYPE vgbel,
           lv_audat TYPE audat,
           lv_ernam TYPE ernam,
           lv_vbelv TYPE vbelv.

    DATA: ls_prcd    TYPE prcd_elements,
          ls_konh    TYPE konh,
          ls_tlic_gs TYPE tlic_gs.

    TYPES:BEGIN OF ty_split_text,
            text(100),
          END OF ty_split_text.
    DATA: lv_amount_text TYPE j_1ig_grossamt_txt,
          ls_split_text  TYPE ty_split_text,
          lt_split_text  TYPE TABLE OF ty_split_text.

    DATA: lv_kunnr  TYPE kunnr,
          lv_branch TYPE brnch,
          lv_bankl  TYPE bankk.

    TYPES : BEGIN OF ty_prcd_elements1,
             kposn TYPE kposn,
             kschl TYPE kschl,
             kbetr TYPE kbetr,
             kwert TYPE kwert,
             kntyp TYPE kntyp,
             kstat TYPE kstat,
             koaid TYPE koaid,
             waerk TYPE waerk,
            END OF ty_prcd_elements1.
    TYPES : BEGIN OF ty_vbrp1,
             vbeln TYPE vbeln_vf,
             posnr TYPE posnr_vf,
             fbuda TYPE fbuda,
            END OF ty_vbrp1.
    TYPES: BEGIN OF ty_value_mapping,
            vmapname(20),
            ext_value(200),
            int_value(200),
      END OF ty_value_mapping .
    DATA :  lt_prcd_elements1 TYPE TABLE OF ty_prcd_elements1,
            ls_prcd_elements1 TYPE ty_prcd_elements1.
    DATA : lt_value_mapping TYPE TABLE OF ty_value_mapping,
           ls_value_mapping TYPE ty_value_mapping,
           lv_surcharge TYPE P LENGTH 16 DECIMALS 5.
    CONSTANTS :   lc_vmap_val_master TYPE char15 VALUE '/AIF/T_MVMAPVAL'.
    DATA:   ls_vbrp1 TYPE ty_vbrp1,
            lt_vbrp1 TYPE TABLE OF ty_vbrp1,
            lv_line TYPE c,
            lv_amount TYPE kwert.

    TRY.
        CALL METHOD super->invoiceset_get_entity
          EXPORTING
            iv_entity_name          = iv_entity_name
            iv_entity_set_name      = iv_entity_set_name
            iv_source_name          = iv_source_name
            it_key_tab              = it_key_tab
            io_request_object       = io_request_object
            io_tech_request_context = io_tech_request_context
            it_navigation_path      = it_navigation_path
          IMPORTING
            er_entity               = er_entity
            es_response_context     = es_response_context.
      CATCH /iwbep/cx_mgw_busi_exception .
      CATCH /iwbep/cx_mgw_tech_exception .
    ENDTRY.

    IF ms_billing_document IS INITIAL.

      CALL METHOD get_billing_document
        RECEIVING
          rs_billing_document = ms_billing_document.
    ENDIF.

*    if ms_billing_document-landtx = lc_country_hu or
*       ms_billing_document-landtx = lc_country_lu or
*       ms_billing_document-landtx = lc_country_be or
*       ms_billing_document-landtx = lc_country_es or
*       ms_billing_document-landtx = lc_country_at or
*       ms_billing_document-landtx = lc_country_it.

    CALL METHOD cl_glo_log_form_utility=>read_accounting_document
      EXPORTING
        iv_billing_doc    = er_entity-billing_document
      IMPORTING
        ev_accounting_doc = er_entity-accounting_document
        ev_company_code   = lv_compcode
        ev_fiscal_year    = lv_fiscalyear.
*    endif.

    TEST-SEAM fill_et1.
    END-TEST-SEAM.

    IF ms_billing_document-landtx = lc_country_es.
      IF er_entity-accounting_document IS NOT INITIAL.
        CALL METHOD cl_glo_log_form_utility=>get_accounting_details
          EXPORTING
            iv_accountdoc  = er_entity-accounting_document
            iv_companycode = lv_compcode
            iv_fiscalyear  = lv_fiscalyear
          IMPORTING
            ev_vatdate     = lv_vatdate.

        IF lv_vatdate IS NOT INITIAL.
          er_entity-vat_date = lv_vatdate.
        ENDIF.
      ENDIF.
    ENDIF.

    IF ms_billing_document-landtx = lc_country_se OR
       ms_billing_document-landtx = lc_country_no OR
       ms_billing_document-landtx = lc_country_fi OR
       ms_billing_document-landtx = lc_country_pl .
* Payment Reference Number in Header for Sweden,Norway,Poland
      IF er_entity-billing_document IS NOT INITIAL.
        CALL METHOD cl_glo_log_form_utility=>get_payment_reference
          EXPORTING
            ev_billingdocument  = er_entity-billing_document
          IMPORTING
            iv_paymentreference = er_entity-payment_reference.
      ENDIF.
    ENDIF.

    IF ms_billing_document-landtx = lc_country_it.
* Goods reciept/Issue Slip Number based on the reference delivery document
* Italy

      CLEAR   ls_refdelivery.
      REFRESH lt_refdelivery.

      IF er_entity-reference_sd_document_category EQ 'J'.
        ls_refdelivery-vbeln = er_entity-reference_sd_document.
        APPEND ls_refdelivery TO lt_refdelivery.

        CLEAR ls_refdelivery.

        CALL METHOD cl_glo_log_form_utility=>get_reference_slip_number
          CHANGING
            ct_referencedelivery = lt_refdelivery.

        IF sy-subrc  = 0.
          READ TABLE lt_refdelivery INTO ls_refdelivery INDEX 1.
          er_entity-reference_slip_number = ls_refdelivery-xabln.
        ENDIF.
        CLEAR ls_refdelivery.
      ENDIF.

*            license no and license date

      SELECT SINGLE * FROM prcd_elements INTO ls_prcd WHERE knumv = ms_billing_document-knumv "#EC CI_ALL_FIELDS_NEEDED
                                                        AND kschl = lc_lcit.

      SELECT SINGLE * FROM konh INTO ls_konh WHERE knumh = ls_prcd-knumh. "#EC CI_ALL_FIELDS_NEEDED

      IF sy-subrc EQ 0.
        IF NOT ls_konh-licno IS INITIAL AND NOT ls_konh-licdt IS INITIAL.
***  Below code is commented due to double maintainence for LICNO
*          SELECT SINGLE * FROM tlic_gs INTO ls_tlic_gs WHERE licno  = ls_konh-licno
*                                    AND   kunnr  = ms_billing_document-kunag.
*          IF sy-subrc NE 0.
** Alte tlic_gs-Sätze haben KUNNR initial. Alter Satz vorhanden ?
*            DATA: da_kunnr_initial LIKE ms_billing_document-kunag.
*            CLEAR da_kunnr_initial.
*
*            SELECT SINGLE * FROM tlic_gs INTO ls_tlic_gs WHERE licno = ls_konh-licno
*                                      AND   kunnr = da_kunnr_initial.
*          ENDIF.
*          IF sy-subrc EQ 0.
*            IF NOT ls_tlic_gs-prnum_nr IS INITIAL AND
*               NOT ls_tlic_gs-prnum_dt IS INITIAL.
          MOVE:
            ls_konh-licno TO er_entity-license_number,
            ls_konh-licdt TO er_entity-license_date.
*            ENDIF.
*          ENDIF.
        ENDIF.
      ENDIF.

      "ODN for PDF
      DATA : lv_blart   TYPE vbrk-blart,
             lv_offnrel TYPE t003_i-offnrel.

      CLEAR:  lv_blart, lv_offnrel.

      SELECT SINGLE blart FROM vbrk INTO lv_blart
        WHERE vbeln = ms_billing_document-vbeln.

      IF sy-subrc EQ 0 AND lv_blart IS NOT INITIAL.
        SELECT SINGLE offnrel FROM t003_i INTO lv_offnrel WHERE
          land1 =  ms_billing_document-land1 AND
          blart  =  lv_blart.
      ENDIF.

      IF lv_offnrel = 'B' OR
          lv_offnrel = 'C'.
      ELSE.
        er_entity-document_reference_id = er_entity-accounting_document.
      ENDIF.
      .
      "ODN for PDF
    ENDIF.

* Country of destination
    er_entity-destination_country = ms_billing_document-land1.


***   Indonesia
    IF ms_billing_document-landtx = lc_country_id.


* Country of destination
*      er_entity-destination_country = ms_billing_document-land1.


* Total Amount In Words
      IF er_entity-total_gross_amount IS NOT INITIAL.
        CALL FUNCTION 'SPELL_AMOUNT'
          EXPORTING
            amount    = er_entity-total_gross_amount
            currency  = er_entity-transaction_currency
*           FILLER    = ' '
            language  = sy-langu
          IMPORTING
            in_words  = lt_words
          EXCEPTIONS
            not_found = 1
            too_large = 2
            OTHERS    = 3.
        IF sy-subrc <> 0.
* Implement suitable error handling here
        ENDIF.

        SELECT SINGLE ktext INTO lv_ktext
               FROM tcurt
               WHERE spras = sy-langu
               AND   waers = er_entity-transaction_currency.

        CONCATENATE lt_words-word lv_ktext INTO lv_words SEPARATED BY ' '.
        TRANSLATE lv_words TO UPPER CASE.

        er_entity-total_amount_in_words = lv_words.
      ENDIF.

* Tax Invoice Signer
      SELECT SINGLE paval
             FROM t001z
             INTO er_entity-tax_invoice_signer
             WHERE bukrs = ms_billing_document-bukrs
             AND   party = 'IDSIGN'.


    ENDIF.


*** Poland : Correction Invoice
    IF  ms_billing_document-landtx = lc_country_pl AND
        ms_billing_document-vbtyp NE 'M'.

      CLEAR: lv_vbeln,
             lv_fkdat,
             lv_augru,
             lv_bezei.

      CALL FUNCTION 'CONVERSION_EXIT_ALPHA_INPUT'                    " Converting billing document number to internal format
        EXPORTING
          input  = ms_billing_document-vbeln
        IMPORTING
          output = lv_vbeln.

      SELECT SINGLE fkdat FROM vbrk                                  " reference invoice date
                    INTO lv_fkdat
                    WHERE vbeln = lv_vbeln.

      SELECT SINGLE augru FROM vbak                                  " order reason or reason for correction
                    INTO lv_augru
                    WHERE vbeln =  er_entity-reference_sd_document.

      SELECT SINGLE bezei FROM tvaut                                 " order reason description
                    INTO lv_bezei
                    WHERE spras = sy-langu
                    AND augru = lv_augru.

      er_entity-referred_vatinvoice_date = lv_fkdat.
      er_entity-sales_order_reason       = lv_augru.
      er_entity-sales_order_reasontext   = lv_bezei.

***     To check whether the correction invoice is differential or credit/debit lines
      CASE er_entity-reference_sd_document_category.                 " Reference SD Document

        WHEN 'K' OR 'L'.                                             "Sales Document(credit/debit memo request)
          CLEAR : lv_auart,
                  lv_vbklt.

          SELECT SINGLE auart FROM vbak                              "Sales Document Type
                        INTO lv_auart
                        WHERE vbeln = er_entity-reference_sd_document.

          IF sy-subrc = 0.
            SELECT SINGLE vbklt FROM tvak
                          INTO lv_vbklt
                          WHERE auart = lv_auart.                    "Sales Document Indicator
            IF lv_vbklt IS INITIAL.
              mv_correction_indicator = 'X'.                       "Differential
            ENDIF.
          ENDIF.


        WHEN 'M' OR '5'.                                             "Billing Document
          mv_correction_indicator = 'X'.                             "Differential

        WHEN 'T'.                                                    "Return Delivery Document
          mv_correction_indicator = 'X'.                             "Differential

        WHEN OTHERS.

      ENDCASE.

      er_entity-correction_indicator = mv_correction_indicator.      "Correction Invoice Type Indicator

      IF ms_billing_document-vbtyp EQ 'O' OR                         "Credit Scenario
         ms_billing_document-vbtyp EQ '6'.

        IF er_entity-tax_amount <> 0.
          er_entity-tax_amount = er_entity-tax_amount * -1.            " Reverse the sign
        ENDIF.

        IF er_entity-total_gross_amount <> 0.
          er_entity-total_gross_amount = er_entity-total_gross_amount * -1.  " Reverse the sign
        ENDIF.

        IF er_entity-total_net_amount <> 0.
          er_entity-total_net_amount = er_entity-total_net_amount * -1.    " Reverse the sign
        ENDIF.

      ENDIF.


    ENDIF.

    TEST-SEAM ts_br.
    END-TEST-SEAM.

    " Brazil:
    " it is necessary to sum the items IBRX as total net value
    " the total gross amoun will be the total net value + the selected header taxes
    IF lo_data_buffer->ms_header-lland = lc_country_br AND ms_billing_document-landtx = lc_country_br.

      CALL METHOD cl_fdp_v3_bd_trans_data_helper=>get_transient_data "get pricing data
        IMPORTING
          et_komv = lt_komv.

      priceconditionse_get_entityset( "get selected header taxes
        EXPORTING
         iv_entity_name = iv_entity_name
         iv_entity_set_name = iv_entity_set_name
         iv_source_name = iv_source_name
         it_filter_select_options = lt_filter_select_options
         it_order = lt_order
         is_paging = ls_paging
         it_navigation_path = it_navigation_path
         it_key_tab = it_key_tab
         iv_filter_string = lv_filter_string
         iv_search_string = lv_search_string
        IMPORTING
         et_entityset = lt_pricecondition
       ).

      DATA lo_billing_output_mngmt TYPE REF TO cl_j1b_billing_output_mngmt.
      CREATE OBJECT lo_billing_output_mngmt.

      lo_billing_output_mngmt->if_j1b_billing_output_mngmt~get_invoice_set_entity(
        EXPORTING
          iv_country                 = lo_data_buffer->ms_header-lland
          it_price_conditions_entity = lt_pricecondition
          it_pricing_data            = lt_komv
        CHANGING
          cr_entity                  = er_entity
      ).

    ENDIF.


*** India
    IF  ms_billing_document-landtx = lc_country_in.
      CLEAR : lv_audat, lv_ernam.
      CLEAR: ls_split_text,
             lt_split_text.
      REFRESH: lt_split_text.
* Amount in words for INR - Change of FM HR_IN_CHG_INR_WRDS to Class method call ER9K8AVWRS
      TRY.
          cl_glo_in_inwords_inr=>amount_in_words(
            EXPORTING
              amt_in_num         = er_entity-total_gross_amount
            IMPORTING
              amt_in_words       = lv_amount_text
          ).CATCH cx_sy_dyn_call_illegal_type.
      ENDTRY.

      IF sy-subrc <> 0.
*      implement suitable error handling here
      ELSE.
        SHIFT lv_amount_text LEFT DELETING LEADING space.                " Deleting the lead spaces
        TRANSLATE lv_amount_text TO LOWER CASE.

        " Start of changing only the first letter of the word to upper case.
        SPLIT lv_amount_text AT space INTO TABLE lt_split_text.

        CLEAR: lv_amount_text.

        LOOP AT lt_split_text INTO ls_split_text.
          TRANSLATE ls_split_text-text+0(1) TO UPPER CASE.
          CONCATENATE lv_amount_text ls_split_text-text INTO lv_amount_text SEPARATED BY space.
          CLEAR: ls_split_text.
        ENDLOOP.
        " End of changing only the first letter of the word to upper case.


        IF ms_billing_document-waerk = 'INR'.
          SHIFT lv_amount_text LEFT DELETING LEADING space.                " Deleting the lead spaces
          er_entity-total_gross_amount_in_words = lv_amount_text.          " Total gross amount in words
        ELSE.
          er_entity-total_gross_amount_in_words = ''.
        ENDIF.
      ENDIF.

      SELECT SINGLE audat ernam FROM vbak INTO (lv_audat, lv_ernam)
                    WHERE vbeln = er_entity-sales_document.
      IF sy-subrc IS INITIAL.
        er_entity-sales_order_date = lv_audat.
        er_entity-contact_name = lv_ernam.
      ENDIF.
      CLEAR : lv_kunnr, lv_bankl, lv_branch.
      IF ms_billing_document-kunrg IS NOT INITIAL.
        lv_kunnr = ms_billing_document-kunrg.
        SELECT SINGLE bankl FROM knbk  INTO lv_bankl WHERE kunnr = lv_kunnr
                                              AND   banks = lc_country_in.
        IF sy-subrc IS INITIAL.
          SELECT SINGLE brnch FROM bnka INTO lv_branch
                                    WHERE banks = lc_country_in
                                    AND bankl =  lv_bankl.
          IF sy-subrc IS INITIAL.
            er_entity-bank_branch = lv_branch.
          ENDIF.
        ENDIF.
      ENDIF.
      "----------- Coding for IRN & QR Code Printing Start---------------------------------------"

***--=================================================================
** QR code Printing
***-================================================================
      DATA :  ls_billing_document TYPE vbrk.
      CONSTANTS : lv_j1iginvrefnum TYPE ddobjname VALUE 'J_1IG_INVREFNUM',
                  lv_edoineinv     TYPE ddobjname VALUE 'EDOINEINV'.
      DATA :  lv_edoc_table  TYPE ddobjname VALUE 'EDOCUMENT'.
      DATA:
        ls_dd02v_invr TYPE dd02v,
        ls_dd02v_edo  TYPE dd02v,
        invrefnum     TYPE REF TO  data,
        edoc2         TYPE REF TO data.
      FIELD-SYMBOLS: <fs_edoc>    TYPE any,
                     <fs_edoinwb> TYPE any.


      CONSTANTS : c_land         TYPE land VALUE 'IN',
                  c_source_typ1  TYPE edoc_source_type VALUE 'SD_INVOICE',
                  c_source_typ2  TYPE edoc_source_type VALUE 'SD_INVNOAC',
                  c_edoc_type    TYPE edoc_type VALUE 'IN_EINV',
                  c_process      TYPE edoc_process VALUE 'INEINV',
                  c_edoc_status  TYPE edoc_status VALUE 'GEN_EINV',
                  c_edoc_status1 TYPE edoc_status VALUE 'COMPLETED'.

      FIELD-SYMBOLS: <fs_invrefnum> TYPE any.
      DATA: lv_response         TYPE string,
            ls_response         TYPE REF TO data,
            ls_comp             TYPE abap_componentdescr,
            ls_stru             TYPE REF TO cl_abap_structdescr,
            lt_comp             TYPE STANDARD TABLE OF abap_componentdescr,
            go_typedescr        TYPE REF TO cl_abap_typedescr,
            gd_fldname          TYPE string,
            ls_data             TYPE REF TO data,
            gs_comp             TYPE abap_compdescr,
            go_strucdesr        TYPE REF TO cl_abap_structdescr,
            go_refdescr         TYPE REF TO cl_abap_refdescr,
            go_strucdesr1       TYPE REF TO cl_abap_structdescr,
            go_refdescr1        TYPE REF TO cl_abap_refdescr,
            gs_comp1            TYPE abap_compdescr,
            ev_field_value(100) TYPE c.

      TYPES:
        BEGIN OF gty_qrcodetext,
          qrcodetext TYPE string, "tline, "txline,
        END OF gty_qrcodetext .

      DATA : ls_qrcodetext TYPE string,
             it_qrcodetext TYPE TABLE OF string.
      DATA : lv_lines TYPE n,
             lv_data  TYPE string.

      CONSTANTS : lc_hash             TYPE char1 VALUE '\', "#
                  lc_hash_conv        TYPE char3 VALUE ' ',
                  lc_module_size      TYPE i     VALUE '20',
                  lc_mode             TYPE char1 VALUE 'U', "U
                  lc_error_correction TYPE char1 VALUE 'M'.
      DATA lv_xstring TYPE xstring.
      DATA lv_encoded_res TYPE string.
      DATA lv_irn TYPE string.
      DATA lv_string TYPE string.
*      DATA str2 TYPE string.
      DATA lt_text   TYPE swxmlcont.
      DATA lv_len TYPE i.

*%*---------------------------Code For B2C Invoice--------------------*%*

*---------------Start of Code for B2C invoice ---------------------
      DATA: lw_kna1  TYPE kna1,
            lw_vbrk  TYPE vbrk,
            lw_bseg  TYPE bseg,
            lw_t012  TYPE t012,
            lw_t012k TYPE t012k,
            lw_vpa   TYPE j_1ig_vpaid,
            lt_vbrp  TYPE TABLE OF vbrp,
            lt_vbpa  TYPE TABLE OF vbpa,
            lw_vbpa  TYPE vbpa,
            Lv_type  TYPE char3.

      SELECT SINGLE * FROM bseg INTO lw_bseg WHERE awkey = er_entity-billing_document AND "#EC CI_ALL_FIELDS_NEEDED "#EC CI_NOFIELD
                                                   koart = 'D'.
      SELECT * FROM vbpa INTO TABLE lt_vbpa WHERE vbeln = er_entity-billing_document. "#EC CI_ALL_FIELDS_NEEDED

      IF lw_bseg-gst_part IS INITIAL.
        READ TABLE lt_vbpa INTO lw_vbpa WITH KEY vbeln = er_entity-billing_document
                                                 parvw = 'RE'.
        SELECT SINGLE * FROM kna1 INTO lw_kna1 WHERE kunnr = lw_vbpa-kunnr AND land1 = 'IN'. "#EC CI_ALL_FIELDS_NEEDED
        IF sy-subrc = 0.
          IF lw_kna1-stcd3 IS INITIAL AND lw_kna1-gst_tds IS INITIAL.
            lv_type = 'B2C'.
          ENDIF.
        ELSE.
          CLEAR: lw_vbpa, lw_kna1.
          READ TABLE lt_vbpa INTO lw_vbpa WITH KEY vbeln = er_entity-billing_document
                                               parvw = 'WE'.
          SELECT SINGLE * FROM kna1 INTO lw_kna1 WHERE kunnr = lw_vbpa-kunnr AND land1 = 'IN'. "#EC CI_ALL_FIELDS_NEEDED
          IF sy-subrc = 0.
            lv_type = 'B2C'.
          ENDIF.
        ENDIF.
      ELSE.
        SELECT SINGLE * FROM kna1 INTO lw_kna1 WHERE kunnr = lw_bseg-kunnr AND land1 = 'IN'. "#EC CI_ALL_FIELDS_NEEDED
        IF sy-subrc = 0.
          IF lw_kna1-stcd3 IS INITIAL AND lw_kna1-gst_tds IS INITIAL.
            lv_type = 'B2C'.
          ENDIF.
        ELSE.
          CLEAR: lw_vbpa, lw_kna1.
          READ TABLE lt_vbpa INTO lw_vbpa WITH KEY vbeln = er_entity-billing_document
                                                   parvw = 'WE'.
          SELECT SINGLE * FROM kna1 INTO lw_kna1 WHERE kunnr = lw_vbpa-kunnr AND land1 = 'IN'. "#EC CI_ALL_FIELDS_NEEDED
          IF sy-subrc = 0.
            lv_type = 'B2C'.
          ENDIF.
        ENDIF.
      ENDIF.
      IF lv_type IS NOT INITIAL.
        SELECT SINGLE * FROM vbrk INTO lw_vbrk WHERE vbeln = er_entity-billing_document. "#EC CI_ALL_FIELDS_NEEDED
        IF sy-subrc IS INITIAL.
          SELECT * FROM vbrp                  "#EC CI_ALL_FIELDS_NEEDED
                   INTO TABLE lt_vbrp
                   WHERE vbeln EQ er_entity-billing_document.
        ENDIF.

        IF lw_bseg-hbkid IS NOT INITIAL AND lw_bseg-hktid IS NOT INITIAL.
*---------------------To Fetch IFSC code
          SELECT SINGLE * FROM t012 INTO lw_t012
                          WHERE bukrs = lw_bseg-bukrs
                           AND  hbkid = lw_bseg-hbkid.
*---------------------To fetch Bank account number
          SELECT SINGLE * FROM t012k INTO lw_t012k "#EC CI_ALL_FIELDS_NEEDED
                          WHERE bukrs = lw_bseg-bukrs
                           AND  hbkid = lw_bseg-hbkid
                           AND hktid = lw_bseg-hktid.

          SELECT SINGLE * FROM j_1ig_vpaid INTO lw_vpa
                            WHERE bukrs = lw_bseg-bukrs
                             AND  hbkid = lw_bseg-hbkid
                             AND  hktid = lw_bseg-hktid
                             AND  vkorg = lw_vbrk-vkorg.

          IF lw_vpa IS NOT INITIAL.
            DATA: lv_upi      TYPE string,
                  lv_gst      TYPE string,
                  lv_bank     TYPE string,
                  lv_acc_name TYPE string,
                  lv_inv_amt  TYPE string,
                  lvs_cgst    TYPE string,
                  lvs_sgst    TYPE string,
                  lvs_igst    TYPE string,
                  lv_tax      TYPE string,
                  lv_gstin    TYPE stcd3,                 "GST Number
                  lv_branc    TYPE j_1bbranc_,         "Bus Partner. "kwert.
                  lv_cgst     TYPE kwert,
                  lv_sgst     TYPE kwert,
                  lv_igst     TYPE kwert.

*----------------------Code to get Supplier GSTIN
            READ TABLE lt_vbrp INTO DATA(lw_vbrp) INDEX 1.

            CALL FUNCTION 'J_1IG_GET_PLANT_DETAILS'
              EXPORTING
                im_werks  = lw_vbrp-werks
                im_bukrs  = lw_bseg-bukrs
              IMPORTING
                ex_branch = lv_branc
                ex_gstin  = lv_gstin.            " Supplier GSTIN

*--------------------Code for TAX Splitting-- CGST SGST CGST
            DATA: gt_konv TYPE TABLE OF prcd_elements,
                  ls_konv TYPE prcd_elements.
            SELECT  * FROM prcd_elements
                INTO TABLE gt_konv
                WHERE knumv EQ lw_vbrk-knumv.
            IF sy-subrc IS INITIAL.
              DATA gt_konp TYPE TABLE OF konp.

              SELECT * FROM konp                   "#EC CI_NO_TRANSFORM
                       INTO TABLE gt_konp
                       FOR ALL ENTRIES IN gt_konv
                       WHERE knumh EQ gt_konv-knumh. "#EC CI_ALL_FIELDS_NEEDED
            ENDIF.
            DATA ls_excdefn TYPE j_1iexcdefn.            "Conditions
            DATA(lv_kalsm) = lw_vbrk-kalsm.
            LOOP AT gt_konv INTO ls_konv." WHERE kposn EQ '000010' .

*----Tax Conditions
              IF ls_konv-koaid EQ 'D'.   " Tax
                CLEAR ls_excdefn.
                SELECT SINGLE *                                       "condition name
                              FROM j_1iexcdefn
                              INTO ls_excdefn
                              WHERE kalsm = lv_kalsm      AND
                                    kschl = ls_konv-kschl.

                IF ls_excdefn-cond_name EQ 'CGSTAR'.                  "CGST
                  DATA(lv_cgst_chl) = ls_konv-kschl.
                ELSEIF ls_excdefn-cond_name EQ 'SGSTAR'.              "SGST
                  DATA(lv_sgst_chl) = ls_konv-kschl.
                ELSEIF ls_excdefn-cond_name EQ 'IGSTAR'.              "IGST
                  DATA(lv_igst_chl) = ls_konv-kschl.
                ENDIF.
              ENDIF.
            ENDLOOP.
            LOOP AT lt_vbrp INTO DATA(ls_vbrp).
*---Calculation for CGST
              CLEAR ls_konv.
              READ TABLE gt_konv INTO ls_konv
                                 WITH KEY kschl = lv_cgst_chl
                                          kposn = ls_vbrp-posnr.
              IF sy-subrc IS INITIAL.
                lv_cgst = lv_cgst + ls_konv-kwert.
              ENDIF.

*--Calculation for SGST
              CLEAR ls_konv.
              READ TABLE gt_konv INTO ls_konv
                                 WITH KEY kschl = lv_sgst_chl
                                          kposn = ls_vbrp-posnr.
              IF sy-subrc IS INITIAL.
                lv_sgst = lv_sgst + ls_konv-kwert.
              ENDIF.

*--calculation for IGST
              CLEAR ls_konv.
              READ TABLE gt_konv INTO ls_konv
                                 WITH KEY kschl = lv_igst_chl
                                          kposn = ls_vbrp-posnr.
              IF sy-subrc IS INITIAL.
                lv_igst = lv_igst + ls_konv-kwert.
              ENDIF.
            ENDLOOP.
            lvs_cgst = lv_cgst.
            CONDENSE lvs_cgst.
            lvs_sgst = lv_sgst.
            CONDENSE lvs_sgst.
            lvs_igst = lv_igst.
            CONDENSE  lvs_igst.
            CONCATENATE '&CGST=' lvs_cgst '&SGST=' lvs_sgst
                        '&IGST=' lvs_igst INTO lv_tax.

            lv_inv_amt = lw_bseg-dmbtr.
            CONCATENATE 'upi://pay?pa=' lw_vpa-j_1ig_vpaddr INTO lv_upi.

            CONCATENATE '&bankac=' lw_t012k-bankn '&ifsc=' lw_t012-bankl INTO lv_bank.

            CONCATENATE '&tn=' lw_vpa-j_1ig_accname '&pn=''&am=' INTO lv_acc_name.

            CONCATENATE '&cu=INR&gstin=' lv_gstin '&inv_no=' er_entity-billing_document
                        '&inv_date=' lw_vbrk-fkdat  INTO lv_gst.

            CONCATENATE lv_upi lv_bank lv_acc_name lv_inv_amt lv_gst lv_tax '&url=-' INTO lv_string.

          ENDIF.
        ENDIF.

      ELSE.
*---------------------------Code To print IRN and QR code in B2B adobe form

        SELECT SINGLE * FROM vbrk INTO ls_billing_document WHERE vbeln = er_entity-billing_document. "#EC CI_ALL_FIELDS_NEEDED
        IF ls_billing_document-fksto = ' '. " check for cancelled invoices
*--------------------------Check for E-documnet table
          CALL FUNCTION 'DDIF_TABL_GET'
            EXPORTING
              name          = lv_edoineinv                " Name of the Table to be Read
              state         = 'A'              " Read Status of the Table
            IMPORTING
              dd02v_wa      = ls_dd02v_edo                " Table Header
            EXCEPTIONS
              illegal_input = 1                " Value not Allowed for Parameter
              OTHERS        = 2.

          IF ls_dd02v_edo-tabname IS NOT INITIAL.

            DATA edoc3 TYPE REF TO data.
            DATA : edoc4   TYPE REF TO data.

            FIELD-SYMBOLS <fs_edoc3> TYPE any.
            FIELD-SYMBOLS <fs_edoineinv> TYPE any.
            FIELD-SYMBOLS <fs_guid1> TYPE any.
            FIELD-SYMBOLS :<fs_edoinev> TYPE any,
                           <fs_irn1>    TYPE any,
                           <fs_qr>      TYPE any,
                           <fs_ebno_einv>    TYPE any,
                           <fs_vf_date_einv> TYPE any,
                           <fs_vf_time_einv> TYPE any,
                           <fs_vt_date_einv> TYPE any,
                           <fs_vt_time_einv> TYPE any,
                           <fs_ackno>    TYPE any,
                           <fs_ackdate>  TYPE any,
                           <fs_acktime>  TYPE any,
                           <fs_transn_einv>  TYPE any,
                           <fs_tgstin_einv>  TYPE any,
                           <fs_vn_einv>  TYPE any.


            CREATE DATA edoc3 TYPE (lv_edoc_table).
            ASSIGN edoc3->* TO <fs_edoc3>.

*--To fetch the Edoc GUID
            SELECT SINGLE * FROM (lv_edoc_table)
              INTO CORRESPONDING FIELDS OF <fs_edoc3>
              WHERE bukrs = ls_billing_document-bukrs
                AND land = c_land
                AND source_type =  c_source_typ1
                AND source_key = ls_billing_document-vbeln
                AND edoc_type = c_edoc_type
                AND proc_status IN (c_edoc_status,c_edoc_status1)
                AND process = c_process.

            TEST-SEAM ts_edoc.
            END-TEST-SEAM.

            IF sy-subrc EQ 0.

              CREATE DATA edoc4 TYPE (lv_edoineinv).
              ASSIGN edoc2->* TO <fs_edoineinv>.
              ASSIGN edoc4->* TO <fs_edoinev>.

              IF <fs_edoc3> IS ASSIGNED.

                ASSIGN COMPONENT 'EDOC_GUID' OF STRUCTURE <fs_edoc3> TO <fs_guid1>.
                IF <fs_guid1> IS ASSIGNED.

                  CLEAR  lv_encoded_res.
                  SELECT SINGLE * FROM (lv_edoineinv)
                    INTO CORRESPONDING FIELDS OF <fs_edoinev>
                    WHERE edoc_guid = <fs_guid1>.

                  ASSIGN COMPONENT 'INV_REG_NUM' OF STRUCTURE <fs_edoinev> TO <fs_irn1>.
                  IF <fs_irn1> IS ASSIGNED.
                    CLEAR er_entity-irn.
                    er_entity-irn = <fs_irn1>.
                  ENDIF.
                  ASSIGN COMPONENT 'QRCODE' OF STRUCTURE <fs_edoinev> TO <fs_qr>.
                  IF <fs_qr> IS ASSIGNED.
                    lv_encoded_res = <fs_qr>.
                  ENDIF.
                  "2302 Hotfix 9 - Start of eWaybill
                  "E-way bill number
                  ASSIGN COMPONENT 'EWBNO' OF STRUCTURE <fs_edoinev> TO <fs_ebno_einv>.
                  IF <fs_ebno_einv> IS ASSIGNED.
                    er_entity-ewb_number = <fs_ebno_einv>.
                  ENDIF.
                  "Valid From Date
                  ASSIGN COMPONENT 'EWB_CREATE_DATE' OF STRUCTURE <fs_edoinev> TO <fs_vf_date_einv>.
                  IF <fs_vf_date_einv> IS ASSIGNED.
                    er_entity-ewb_validfrom_date = <fs_vf_date_einv>.
                  ENDIF.
                  "Valid From Time
                  ASSIGN COMPONENT 'EWB_CREATE_TIME' OF STRUCTURE <fs_edoinev> TO <fs_vf_time_einv>.
                  IF  <fs_vf_time_einv> IS ASSIGNED.
                    er_entity-ewb_validfrom_time = <fs_vf_time_einv>.
                  ENDIF.
                  "Valid To Date
                  ASSIGN COMPONENT 'EWB_VALID_END_DATE' OF STRUCTURE <fs_edoinev> TO <fs_vt_date_einv>.
                  IF <fs_vt_date_einv> IS ASSIGNED.
                    er_entity-ewb_validto_date = <fs_vt_date_einv>.
                  ENDIF.
                  "Valid To Time
                  ASSIGN COMPONENT 'EWB_VALID_ENDAT' OF STRUCTURE <fs_edoinev> TO <fs_vt_time_einv>.
                  IF  <fs_vt_time_einv> IS ASSIGNED.
                    er_entity-ewb_validto_time = <fs_vt_time_einv>.
                  ENDIF.
                  "2302 Hotfix 9 - End of eWaybill
                  "CFD - 2302.4
                  "Adding ACK Number
                  ASSIGN COMPONENT 'ACK_NO' OF STRUCTURE <fs_edoinev> TO <fs_ackno>.
                  IF <fs_ackno> IS ASSIGNED.
                     er_entity-ack_number = <fs_ackno>.
                  ENDIF.
                  ASSIGN COMPONENT 'ACK_DATE' OF STRUCTURE <fs_edoinev> TO <fs_ackdate>.
                  IF <fs_ackdate> IS ASSIGNED.
                     er_entity-ack_date = <fs_ackdate>.
                  ENDIF.
                  ASSIGN COMPONENT 'ACK_TIME' OF STRUCTURE <fs_edoinev> TO <fs_acktime>.
                  IF <fs_acktime> IS ASSIGNED.
                     er_entity-ack_time = <fs_acktime>.
                  ENDIF.
                  "Transporter name
                  ASSIGN COMPONENT 'EWB_TRANS_NAME' OF STRUCTURE <fs_edoinev> TO <fs_transn_einv>.
                  IF  <fs_Transn_einv> IS ASSIGNED.
                    er_entity-transporter_name = <fs_Transn_einv>.
                  ENDIF.
                  "Transporter GSTIN
                  ASSIGN COMPONENT 'EWB_TRANS_GSTIN' OF STRUCTURE <fs_edoinev> TO <fs_tgstin_einv>.
                  IF  <fs_tgstin_einv> IS ASSIGNED.
                    er_entity-transporter_gstin = <fs_tgstin_einv>.
                  ENDIF.
                  "Vehicle Number
                  ASSIGN COMPONENT 'VEHICLE_NO' OF STRUCTURE <fs_edoinev> TO <fs_vn_einv>.
                  IF  <fs_vn_einv> IS ASSIGNED.
                    er_entity-vehicle_number = <fs_vn_einv>.
                  ENDIF.
                  "End 2302.04 CFD

                  CLEAR lv_string.
                  DATA(lv_string_edoc) = lv_encoded_res.
                  lv_string = lv_string_edoc.
                ENDIF.
              ENDIF.
            ENDIF.
          ENDIF.
          "---------------- Check For Invoice reference Table "J_1IG_INVREFNUM"

          IF ( ls_dd02v_edo-tabname IS NOT INITIAL AND <fs_edoc3> IS INITIAL ) OR  ls_dd02v_edo-tabname IS INITIAL .
            CALL FUNCTION 'DDIF_TABL_GET'
              EXPORTING
                name          = lv_j1iginvrefnum                " Name of the Table to be Read
                state         = 'A'              " Read Status of the Table
              IMPORTING
                dd02v_wa      = ls_dd02v_invr                  " Table Header
              EXCEPTIONS
                illegal_input = 1                " Value not Allowed for Parameter
                OTHERS        = 2.

            IF ls_dd02v_invr-tabname IS NOT INITIAL.

              CREATE DATA invrefnum TYPE (lv_j1iginvrefnum).
              ASSIGN invrefnum->* TO <fs_invrefnum>.

              SELECT SINGLE *
                        FROM (lv_j1iginvrefnum)
                        INTO CORRESPONDING FIELDS OF <fs_invrefnum>
                        WHERE docno = ls_billing_document-vbeln.

              IF <fs_invrefnum> IS ASSIGNED AND sy-subrc = 0.

                CLEAR lv_response.
                ASSIGN COMPONENT 'SIGNED_QRCODE' OF STRUCTURE <fs_invrefnum> TO FIELD-SYMBOL(<lv_encoded_res>).

                ASSIGN COMPONENT 'IRN' OF STRUCTURE <fs_invrefnum> TO FIELD-SYMBOL(<lv_irn>).
                "Adding ACK Details CFD 2023.04
                ASSIGN COMPONENT 'ACK_NO' OF STRUCTURE <fs_invrefnum> TO FIELD-SYMBOL(<lv_ackno>).
                 er_entity-ack_number = <lv_ackno>.
                ASSIGN COMPONENT 'ACK_DATE' OF STRUCTURE <fs_invrefnum> TO FIELD-SYMBOL(<lv_ackdate>).
                REPLACE ALL OCCURRENCES OF SUBSTRING '-' IN <lv_ackdate> WITH ''.
                 er_entity-ack_date = <lv_ackdate>.
                 CONCATENATE <lv_ackdate>+9(02) <lv_ackdate>+12(02) <lv_ackdate>+15(02) INTO er_entity-ack_time.
                "End CFD 2023.04

                CLEAR er_entity-irn.
                er_entity-irn = <lv_irn>.

                CLEAR lv_string.
                lv_string = <lv_encoded_res>.
              ENDIF.
            ENDIF.
          ENDIF.
        ENDIF.
      ENDIF.

*eWay bill
      DATA: ls_dd02v_ewb TYPE dd02v,
            edoc_ewb1    TYPE REF TO data,
            edoc_ewb2    TYPE REF TO data.

      CONSTANTS: c_edoinewb       TYPE ddobjname   VALUE 'EDOINEWB',
                 c_j_1ig_ewaybill TYPE ddobjname   VALUE 'J_1IG_EWAYBILL',
                 c_edoc_type_ewb  TYPE edoc_type   VALUE 'IN_EWB',
                 c_proc_status1   TYPE edoc_status VALUE 'EWB_GEN',
                 c_proc_status2   TYPE edoc_status VALUE 'COMPLETED',
                 c_proc_status3   TYPE edoc_status VALUE 'MODIF_APPR',
                 c_proc_status4   TYPE edoc_status VALUE 'EWB_SLIP'.

      FIELD-SYMBOLS: <fs_edoc_ewb>    TYPE any,
                     <fs_edoinwb_ewb> TYPE any,
                     <fs_guid_ewb>    TYPE any,
                     <fs_ebno_ewb>    TYPE any,
                     <fs_vf_date>     TYPE any,
                     <fs_vf_time>     TYPE any,
                     <fs_vt_date>     TYPE any,
                     <fs_vt_time>     TYPE any,
                     <fs_transn_ewb>  TYPE any,
                     <fs_tgstin_ewb>  TYPE any,
                     <fs_vn_ewb>      TYPE any.

      CLEAR: ls_dd02v_ewb, edoc_ewb1, edoc_ewb2.

      "Check for E-document table
      CALL FUNCTION 'DDIF_TABL_GET'
        EXPORTING
          name          = c_edoinewb           " Name of the Table to be Read
          state         = 'A'                  " Read Status of the Table
        IMPORTING
          dd02v_wa      = ls_dd02v_ewb         " Table Header
        EXCEPTIONS
          illegal_input = 1                    " Value not Allowed for Parameter
        OTHERS          = 2.

      IF ls_dd02v_ewb-tabname IS NOT INITIAL.
        "--To fetch the Edoc GUID
        CREATE DATA edoc_ewb1 TYPE (lv_edoc_table).
        ASSIGN edoc_ewb1->* TO <fs_edoc_ewb>.
        SELECT SINGLE * FROM (lv_edoc_table) INTO CORRESPONDING FIELDS OF <fs_edoc_ewb> WHERE bukrs = ms_billing_document-bukrs
                                                                AND land = c_land
                                                                AND ( source_type =  c_source_typ1 OR  source_type = c_source_typ2 )
                                                                AND source_key = ms_billing_document-vbeln
                                                                AND edoc_type = c_edoc_type_ewb
                                                                AND ( proc_status = c_proc_status1 OR proc_status = c_proc_status2
                                                                 OR   proc_status = c_proc_status3 OR proc_status = c_proc_status4 ).
        IF sy-subrc EQ 0.
          "pass the company code from the billing document
          CREATE DATA edoc_ewb2 TYPE (c_edoinewb).
          ASSIGN edoc_ewb2->* TO <fs_edoinwb_ewb>.
          IF <fs_edoc_ewb> IS ASSIGNED.
            ASSIGN COMPONENT 'EDOC_GUID' OF STRUCTURE <fs_edoc_ewb> TO <fs_guid_ewb>.
            IF <fs_guid_ewb> IS ASSIGNED.
              SELECT SINGLE * FROM (c_edoinewb) INTO CORRESPONDING FIELDS OF <fs_edoinwb_ewb> WHERE edoc_guid = <fs_guid_ewb>.
              IF <fs_edoinwb_ewb> IS ASSIGNED.
                "Assign the edocument variables
                ASSIGN COMPONENT 'EWB_NUMBER' OF STRUCTURE <fs_edoinwb_ewb> TO <fs_ebno_ewb>.
                "E-way bill number
                IF <fs_ebno_ewb> IS ASSIGNED.
                  er_entity-ewb_number = <fs_ebno_ewb>.
                ENDIF.
                "Valid From Date
                ASSIGN COMPONENT 'EWB_CREATE_DATE' OF STRUCTURE <fs_edoinwb_ewb> TO <fs_vf_date>.
                IF <fs_vf_date> IS ASSIGNED.
                  er_entity-ewb_validfrom_date = <fs_vf_date>.
                ENDIF.
                "Valid From Time
                ASSIGN COMPONENT 'EWB_CREATE_TIME' OF STRUCTURE <fs_edoinwb_ewb> TO <fs_vf_time>.
                IF  <fs_vf_time> IS ASSIGNED.
                  er_entity-ewb_validfrom_time = <fs_vf_time>.
                ENDIF.
                "Valid To Date
                ASSIGN COMPONENT 'EWB_VALID_END_DATE' OF STRUCTURE <fs_edoinwb_ewb> TO <fs_vt_date>.
                IF <fs_vt_date> IS ASSIGNED.
                  er_entity-ewb_validto_date = <fs_vt_date>.
                ENDIF.
                "Valid To Time
                ASSIGN COMPONENT 'EWB_VALID_ENDAT' OF STRUCTURE <fs_edoinwb_ewb> TO <fs_vt_time>.
                IF  <fs_vt_time> IS ASSIGNED.
                  er_entity-ewb_validto_time = <fs_vt_time>.
                ENDIF.
                "2302.04 CFD
                "Transporter name
                ASSIGN COMPONENT 'EWB_TRANS_NAME' OF STRUCTURE <fs_edoinwb_ewb> TO <fs_transn_ewb>.
                IF  <fs_Transn_ewb> IS ASSIGNED.
                  er_entity-transporter_name = <fs_Transn_ewb>.
                ENDIF.
                "Transporter GSTIN
                ASSIGN COMPONENT 'EWB_TRANS_GSTIN' OF STRUCTURE <fs_edoinwb_ewb> TO <fs_tgstin_ewb>.
                IF  <fs_tgstin_ewb> IS ASSIGNED.
                  er_entity-transporter_gstin = <fs_tgstin_ewb>.
                ENDIF.
                "Vehicle Number
                ASSIGN COMPONENT 'VEHICLE_NO' OF STRUCTURE <fs_edoinwb_ewb> TO <fs_vn_ewb>.
                IF  <fs_vn_ewb> IS ASSIGNED.
                   er_entity-vehicle_number = <fs_vn_ewb>.
                ENDIF.
                "End 2302.04 CFD
              ENDIF.
            ENDIF.
          ENDIF.
          UNASSIGN: <fs_edoinwb_ewb>, <fs_ebno_ewb>, <fs_edoc_ewb>, <fs_guid_ewb>.
          UNASSIGN: <fs_vf_date>, <fs_vf_time>, <fs_vt_date>, <fs_vt_time>.
        ENDIF.
      ENDIF.
      IF er_entity-ewb_number IS INITIAL.
        CLEAR: ls_dd02v_ewb.
        "Check for E-document table
        CALL FUNCTION 'DDIF_TABL_GET'
        EXPORTING
          name          = c_j_1ig_ewaybill    " Name of the Table to be Read
          state         = 'A'                  " Read Status of the Table
        IMPORTING
          dd02v_wa      = ls_dd02v_ewb         " Table Header
        EXCEPTIONS
          illegal_input = 1                    " Value not Allowed for Parameter
        OTHERS          = 2.

        IF ls_dd02v_ewb-tabname IS NOT INITIAL.
          DATA: ls_j1ig_ewaybill TYPE j_1ig_ewaybill.
          "Fetch E-Way bill details
          SELECT SINGLE ebillno vdfmdate vdfmtime vdtodate vdtotime
          FROM j_1ig_ewaybill INTO CORRESPONDING FIELDS OF ls_j1ig_ewaybill
          WHERE docno = ms_billing_document-vbeln AND status = 'A'.
          IF sy-subrc = 0.
            er_entity-ewb_number         = ls_j1ig_ewaybill-ebillno.
            er_entity-ewb_validfrom_date = ls_j1ig_ewaybill-vdfmdate.
            er_entity-ewb_validfrom_time = ls_j1ig_ewaybill-vdfmtime.
            er_entity-ewb_validto_date   = ls_j1ig_ewaybill-vdtodate.
            er_entity-ewb_validto_time   = ls_j1ig_ewaybill-vdtotime.
          ENDIF.
        ENDIF.
      ENDIF.
*eWay bill

      TEST-SEAM ts_str.
      END-TEST-SEAM.
      IF lv_string IS NOT INITIAL.
        ls_qrcodetext = lv_string.

        APPEND ls_qrcodetext TO it_qrcodetext.
        CLEAR : lv_data.

        LOOP AT it_qrcodetext INTO ls_qrcodetext.
          CONCATENATE lv_data ls_qrcodetext INTO lv_data.
          CLEAR ls_qrcodetext.
        ENDLOOP.

        REPLACE ALL OCCURRENCES OF lc_hash IN lv_data WITH lc_hash_conv.

        CALL METHOD cl_rstx_barcode_renderer=>qr_code
          EXPORTING
            i_module_size      = lc_module_size
            i_mode             = lc_mode
            i_error_correction = lc_error_correction
            i_barcode_text     = lv_data
          IMPORTING
            e_bitmap           = er_entity-qrcode_bitmap.

      ENDIF.
      "---------- Coding for IRN & QR Code Printing End------------------------------------------"

    ENDIF.

    "Usage Measurement Enabled for Romania
    IF  ms_billing_document-landtx = lc_country_ro.
      CALL METHOD cl_glo_log_usage=>call_susage_insert
        EXPORTING
          i_feature = 'GS_GSCBEMEAE_2555_1'.

    ENDIF.

    "Thailand-CE1908
    IF  ms_billing_document-landtx = lc_country_th.

      "populate the customer branch code field
      SELECT SINGLE j_1tpbupl FROM vbrk INTO er_entity-customer_branch_code WHERE vbeln = ms_billing_document-vbeln.
      IF sy-subrc <> 0.
        CLEAR er_entity-customer_branch_code.
      ENDIF.
      "remove leading 0 from ODN number
      SHIFT er_entity-document_reference_id LEFT DELETING LEADING '0'.
      IF er_entity-total_gross_amount IS NOT INITIAL.
        CALL FUNCTION 'SPELL_AMOUNT'
          EXPORTING
            amount    = er_entity-total_gross_amount
            currency  = er_entity-transaction_currency
*           FILLER    = ' '
            language  = sy-langu
          IMPORTING
            in_words  = lt_words
          EXCEPTIONS
            not_found = 1
            too_large = 2
            OTHERS    = 3.
        IF sy-subrc <> 0.
* Implement suitable error handling here
        ENDIF.

        SELECT SINGLE ktext INTO lv_ktext
               FROM tcurt
               WHERE spras = sy-langu
               AND   waers = er_entity-transaction_currency.

        CONCATENATE lt_words-word lv_ktext lt_words-decword lc_curr_th INTO lv_words SEPARATED BY ' '.
        TRANSLATE lv_words TO UPPER CASE.

        er_entity-total_amount_in_words = lv_words.
      ENDIF.
      "for debit note, credit note
      IF er_entity-sd_document_category = 'O' OR er_entity-sd_document_category = 'P'.


        CALL FUNCTION 'CONVERSION_EXIT_ALPHA_INPUT'                    " Converting billing document number to internal format
          EXPORTING
            input  = er_entity-reference_sd_document
          IMPORTING
            output = lv_vbeln.
        SELECT SINGLE augru FROM vbak                                  " order reason or reason for correction
                      INTO er_entity-sales_order_reason
                      WHERE vbeln =  lv_vbeln.
        IF sy-subrc = 0.
          SELECT SINGLE bezei FROM tvaut                                 " order reason description
                        INTO er_entity-sales_order_reasontext
                        WHERE spras = sy-langu
                        AND augru = er_entity-sales_order_reason.
        ENDIF.
        "fetching original invoice
        SELECT SINGLE vgbel FROM vbak INTO lv_vgbel WHERE vbeln = lv_vbeln.
        IF sy-subrc = 0.
          SELECT SINGLE xblnr fkdat FROM vbrk                                  " reference invoice date
                        INTO ( er_entity-referred_vatinvoice, er_entity-referred_vatinvoice_date )
                        WHERE vbeln = lv_vgbel.
          SHIFT er_entity-referred_vatinvoice LEFT DELETING LEADING '0'.
        ENDIF.


      ENDIF.

    ENDIF.

    "Czech Republic - CE1908
    IF  ms_billing_document-landtx = lc_country_cz OR ms_billing_document-land1 = lc_country_cz.
      "Usage Measurement Enabled for CZ
      CALL METHOD cl_glo_log_usage=>call_susage_insert
        EXPORTING
          i_feature = 'GS_GSCBEMEAE_3093_1'.

      IF er_entity-sd_document_category = 'O' OR er_entity-sd_document_category = 'P'.

        CALL FUNCTION 'CONVERSION_EXIT_ALPHA_INPUT'                    " Converting billing document number to internal format
          EXPORTING
            input  = er_entity-reference_sd_document
          IMPORTING
            output = lv_vbeln.

        SELECT SINGLE vbelv FROM vbfa INTO lv_vbelv WHERE vbeln = lv_vbeln. "#EC CI_NOFIELD "Fetching sales order number using credit/debit memo request number
        IF sy-subrc = 0.
          SELECT SINGLE vbeln FROM vbfa                          " Fetching Original invoice number using Sales order number
                        INTO er_entity-referred_vatinvoice
                        WHERE vbelv = lv_vbelv AND vbtyp_n = 'M'.
          SHIFT er_entity-referred_vatinvoice LEFT DELETING LEADING '0'.
        ENDIF.
        " Logic to fetch Reason for correction for Credit/Debit memo
        SELECT SINGLE augru FROM vbak                                  " order reason or reason for correction
               INTO er_entity-sales_order_reason
               WHERE vbeln =  lv_vbeln.
        IF sy-subrc = 0.
          SELECT SINGLE bezei FROM tvaut                                 " order reason description
                        INTO er_entity-sales_order_reasontext
                        WHERE spras = sy-langu
                        AND augru = er_entity-sales_order_reason.
        ENDIF.
      ENDIF.
    ENDIF.

*    IF  ms_billing_document-landtx = lc_country_ae."1908 HFC02 United Arab Emirates Billing Form
*      IF er_entity-total_gross_amount IS NOT INITIAL.
*        CALL FUNCTION 'SPELL_AMOUNT'
*          EXPORTING
*            amount    = er_entity-total_gross_amount
*            currency  = er_entity-transaction_currency
**           FILLER    = ' '
*            language  = sy-langu
*          IMPORTING
*            in_words  = lt_words
*          EXCEPTIONS
*            not_found = 1
*            too_large = 2
*            OTHERS    = 3.
*        IF sy-subrc <> 0.
** Implement suitable error handling here
*        ENDIF.
*
*        SELECT SINGLE ktext INTO lv_ktext
*               FROM tcurt
*               WHERE spras = sy-langu
*               AND   waers = er_entity-transaction_currency.
*
*        CONCATENATE lt_words-word lv_ktext lt_words-decword TEXT-fil INTO lv_words SEPARATED BY ' '.
*        TRANSLATE lv_words TO UPPER CASE.
*
*        er_entity-total_amount_in_words = lv_words.
*      ENDIF.
*      er_entity-total_net_amount = ms_billing_document-netwr.
*    ENDIF.
*
*    IF  ms_billing_document-landtx = lc_country_sa."1908 HFC02 Saudi Arabia Billing Form
*      IF er_entity-total_gross_amount IS NOT INITIAL.
*        CALL FUNCTION 'SPELL_AMOUNT'
*          EXPORTING
*            amount    = er_entity-total_gross_amount
*            currency  = er_entity-transaction_currency
**           FILLER    = ' '
*            language  = sy-langu
*          IMPORTING
*            in_words  = lt_words
*          EXCEPTIONS
*            not_found = 1
*            too_large = 2
*            OTHERS    = 3.
*        IF sy-subrc <> 0.
** Implement suitable error handling here
*        ENDIF.
*
*        SELECT SINGLE ktext INTO lv_ktext
*               FROM tcurt
*               WHERE spras = sy-langu
*               AND   waers = er_entity-transaction_currency.
*
*        CONCATENATE lt_words-word lv_ktext lt_words-decword TEXT-hal INTO lv_words SEPARATED BY ' '.
*        TRANSLATE lv_words TO UPPER CASE.
*
*        er_entity-total_amount_in_words = lv_words.
*      ENDIF.
*      er_entity-total_net_amount = ms_billing_document-netwr.
*     ENDIF.

    IF  ms_billing_document-landtx = lc_country_ae OR
        ms_billing_document-landtx = lc_country_om OR
        ms_billing_document-landtx = lc_country_sa OR
        ms_billing_document-landtx = lc_country_eg.
     er_entity-exchange_rate = er_entity-abslt_accounting_exchange_rate.

    SELECT vbeln posnr fbuda FROM vbrp INTO TABLE lt_vbrp1 WHERE
                                  vbeln = ms_billing_document-vbeln.
    SORT lt_vbrp1 BY fbuda.
    DELETE ADJACENT DUPLICATES FROM lt_vbrp1 COMPARING fbuda.
    DESCRIBE TABLE lt_vbrp1 LINES lv_line.
    IF lv_line = 1.
      READ TABLE lt_vbrp1 INTO ls_vbrp1 WITH KEY vbeln = ms_billing_document-vbeln.
      IF ls_vbrp1 IS NOT INITIAL.
        er_entity-supply_date =  ls_vbrp1-fbuda.
      ENDIF.
    ENDIF.
      IF NOT er_entity IS INITIAL.
         "Convert to Local Currency
         DATA: lv_local_amount_ar  TYPE kwert,
               lv_exchange_rate_ar TYPE string,
               loc_curr_ar TYPE waerl.

         IF ms_billing_document-landtx = lc_country_ae.
             er_entity-loc_curr = 'AED'.
         ELSEIF ms_billing_document-landtx = lc_country_sa.
             er_entity-loc_curr = 'SAR'.
         ELSEIF ms_billing_document-landtx = lc_country_om.
             er_entity-loc_curr = 'OMR'.
         ELSEIF ms_billing_document-landtx = lc_country_eg.
            er_entity-loc_curr = 'EGP'.
            SELECT vmapname int_value ext_value FROM (lc_vmap_val_master)
               INTO CORRESPONDING FIELDS OF TABLE lt_value_mapping
               WHERE ns = '/EDOEG'  AND vmapname = 'CONDITION_TYPES'.
         ENDIF.
         er_entity-total_net_amount = ms_billing_document-netwr.
         IF er_entity-transaction_currency NE er_entity-loc_curr.
           IF er_entity-tax_amount IS NOT INITIAL.
             CALL FUNCTION 'CONVERT_TO_LOCAL_CURRENCY'
               EXPORTING
                 date             = er_entity-billing_document_date
                 foreign_amount   = er_entity-tax_amount
                 foreign_currency = er_entity-transaction_currency
                 local_currency   = er_entity-loc_curr
               IMPORTING
                 exchange_rate    = lv_exchange_rate_ar
                 local_amount     = lv_local_amount_ar
               EXCEPTIONS
                 no_rate_found    = 1
                 overflow         = 2
                 no_factors_found = 3
                 no_spread_found  = 4
                 derived_2_times  = 5
                 OTHERS           = 6.
             IF sy-subrc <> 0.
*      Implement suitable error handling here
             ENDIF.
           ENDIF.
           er_entity-condition_amount_loc_curr = lv_local_amount_ar.
           CLEAR: lv_local_amount_ar, lv_exchange_rate_ar.

           IF er_entity-total_net_amount IS NOT INITIAL.
             CALL FUNCTION 'CONVERT_TO_LOCAL_CURRENCY'
               EXPORTING
                 date             = er_entity-billing_document_date
                 foreign_amount   = er_entity-total_net_amount
                 foreign_currency = er_entity-transaction_currency
                 local_currency   = er_entity-loc_curr
               IMPORTING
                 exchange_rate    = lv_exchange_rate_ar
                 local_amount     = lv_local_amount_ar
               EXCEPTIONS
                 no_rate_found    = 1
                 overflow         = 2
                 no_factors_found = 3
                 no_spread_found  = 4
                 derived_2_times  = 5
                 OTHERS           = 6.
             IF sy-subrc <> 0.
*      Implement suitable error handling here
             ENDIF.
           ENDIF.
           er_entity-total_net_amount_locurr = lv_local_amount_ar.
           CLEAR: lv_local_amount_ar, lv_exchange_rate_ar.


           IF er_entity-total_gross_amount IS NOT INITIAL.
             CALL FUNCTION 'CONVERT_TO_LOCAL_CURRENCY'
               EXPORTING
                 date             = er_entity-billing_document_date
                 foreign_amount   = er_entity-total_gross_amount
                 foreign_currency = er_entity-transaction_currency
                 local_currency   = er_entity-loc_curr
               IMPORTING
                 exchange_rate    = lv_exchange_rate_ar
                 local_amount     = lv_local_amount_ar
               EXCEPTIONS
                 no_rate_found    = 1
                 overflow         = 2
                 no_factors_found = 3
                 no_spread_found  = 4
                 derived_2_times  = 5
                 OTHERS           = 6.
             IF sy-subrc <> 0.
*      Implement suitable error handling here
             ENDIF.
           ENDIF.

           er_entity-total_gross_amount_locurr = lv_local_amount_ar.
           CLEAR: lv_local_amount_ar, lv_exchange_rate_ar.
         ELSE.
           er_entity-condition_amount_loc_curr = er_entity-tax_amount.
           er_entity-total_net_amount_locurr = er_entity-total_net_amount.
           er_entity-total_gross_amount_locurr = er_entity-total_gross_amount.
         ENDIF.
         CALL FUNCTION 'SPELL_AMOUNT'
           EXPORTING
             amount    = er_entity-total_gross_amount_locurr
             currency  = er_entity-loc_curr
*            FILLER    = ' '
             language  = sy-langu
           IMPORTING
             in_words  = lt_words
           EXCEPTIONS
             not_found = 1
             too_large = 2
             OTHERS    = 3.
         IF sy-subrc <> 0.
*      Implement suitable error handling here
         ENDIF.
         SELECT SINGLE ktext INTO lv_ktext
                FROM tcurt
                WHERE spras = sy-langu
                AND   waers = er_entity-loc_curr.
         IF ms_billing_document-landtx = lc_country_ae.
           IF sy-langu = 'A'.
             CONCATENATE lt_words-word lv_ktext lt_words-decword  lo_curr_ae INTO lv_words SEPARATED BY ' '.
             ELSE.
             CONCATENATE lt_words-word lv_ktext lt_words-decword  lc_curr_ae INTO lv_words SEPARATED BY ' '.
           ENDIF.

         ELSEIF ms_billing_document-landtx = lc_country_om.
           IF sy-langu = 'A'.
             CONCATENATE lt_words-word lv_ktext lt_words-decword  lo_curr_om INTO lv_words SEPARATED BY ' '.
             ELSE.
             CONCATENATE lt_words-word lv_ktext lt_words-decword  lc_curr_om INTO lv_words SEPARATED BY ' '.
           ENDIF.

         ELSEIF ms_billing_document-landtx = lc_country_sa.
           IF sy-langu = 'A'.
            CONCATENATE lt_words-word lv_ktext lt_words-decword  lo_curr_sa INTO lv_words SEPARATED BY ' '.
            ELSE.
            CONCATENATE lt_words-word lv_ktext lt_words-decword  lc_curr_sa INTO lv_words SEPARATED BY ' '.
           ENDIF.
         ENDIF.
*         CONCATENATE lt_words-word lv_ktext lt_words-decword  loc_curr_ar INTO lv_words SEPARATED BY ' '.
         TRANSLATE lv_words TO UPPER CASE.

         er_entity-total_amount_in_words = lv_words.
*        Discount & Other charges Calculation
           SELECT kposn kschl kbetr kwert kntyp kstat koaid waerk FROM prcd_elements INTO TABLE lt_prcd_elements1
            WHERE knumv = ms_billing_document-knumv
              AND kinak  = ' '
              AND koaid in ( 'A','B','W' ).
             IF lt_prcd_elements1 IS NOT INITIAL.
              CLEAR lv_surcharge.
              LOOP AT lt_prcd_elements1 INTO ls_prcd_elements1.
               IF ls_prcd_elements1-kwert LT 0 AND ls_prcd_elements1-kntyp = '' AND ls_prcd_elements1-kstat = '' AND ls_prcd_elements1-koaid = 'A'.
                   ls_prcd_elements1-kwert =  -1 * ls_prcd_elements1-kwert .
                   er_entity-total_discount = er_entity-total_discount + ls_prcd_elements1-kwert .
               ELSEIF ls_prcd_elements1-kstat = '' AND ls_prcd_elements1-koaid = 'B'.
                   er_entity-total_sales_amount =  er_entity-total_sales_amount + ls_prcd_elements1-kwert.
               ELSEIF ls_prcd_elements1-kwert GT 0 AND ls_prcd_elements1-kstat = '' AND ls_prcd_elements1-koaid = 'A'.
                 IF ms_billing_document-landtx = lc_country_eg.
                   READ TABLE lt_value_mapping INTO ls_value_mapping WITH KEY ext_value = ls_prcd_elements1-kschl.
                    IF sy-subrc = 0.
                      er_entity-total_other_charges =  er_entity-total_other_charges + ls_prcd_elements1-kwert.
                    ELSE.
                      lv_surcharge = lv_surcharge + ls_prcd_elements1-kwert.
                    ENDIF.
                  ELSE.
                    er_entity-total_other_charges =  er_entity-total_other_charges + ls_prcd_elements1-kwert.
                 ENDIF.

               ELSEIF ls_prcd_elements1-kntyp = 'D' AND ls_prcd_elements1-koaid = 'W'.
                    er_entity-total_wth = er_entity-total_wth + ls_prcd_elements1-kwert.
               ENDIF.
               CLEAR ls_prcd_elements1.
               ENDLOOP.
               IF  lv_surcharge IS NOT INITIAL.
                er_entity-total_sales_amount =  er_entity-total_sales_amount + lv_surcharge.
               ENDIF.
              ENDIF.
              IF er_entity-transaction_currency NE er_entity-loc_curr.
                CLEAR: lv_local_amount_ar, lv_exchange_rate_ar.
                IF er_entity-total_discount IS NOT INITIAL.
                 CALL FUNCTION 'CONVERT_TO_LOCAL_CURRENCY'
                       EXPORTING
                         date             = er_entity-billing_document_date
                         foreign_amount   = er_entity-total_discount
                         foreign_currency = er_entity-transaction_currency
                         local_currency   = er_entity-loc_curr
                       IMPORTING
                         exchange_rate    = lv_exchange_rate_ar
                         local_amount     = lv_local_amount_ar
                       EXCEPTIONS
                         no_rate_found    = 1
                         overflow         = 2
                         no_factors_found = 3
                         no_spread_found  = 4
                         derived_2_times  = 5
                         OTHERS           = 6.
                    IF sy-subrc <> 0.
*      Implement suitable error handling here
                    ENDIF.
                    er_entity-total_discount_loccurr = lv_local_amount_ar.
                    CLEAR: lv_local_amount_ar, lv_exchange_rate_ar.
                 ENDIF.
                 IF er_entity-total_other_charges IS NOT INITIAL.
                   CALL FUNCTION 'CONVERT_TO_LOCAL_CURRENCY'
                       EXPORTING
                         date             = er_entity-billing_document_date
                         foreign_amount   = er_entity-total_other_charges
                         foreign_currency = er_entity-transaction_currency
                         local_currency   = er_entity-loc_curr
                       IMPORTING
                         exchange_rate    = lv_exchange_rate_ar
                         local_amount     = lv_local_amount_ar
                       EXCEPTIONS
                         no_rate_found    = 1
                         overflow         = 2
                         no_factors_found = 3
                         no_spread_found  = 4
                         derived_2_times  = 5
                         OTHERS           = 6.
                    IF sy-subrc <> 0.
*      Implement suitable error handling here
                    ENDIF.
                    er_entity-total_other_charges_loccurr = lv_local_amount_ar.
                    CLEAR: lv_local_amount_ar, lv_exchange_rate_ar.
                 ENDIF.
                 IF er_entity-total_sales_amount IS NOT INITIAL.
                   CALL FUNCTION 'CONVERT_TO_LOCAL_CURRENCY'
                       EXPORTING
                         date             = er_entity-billing_document_date
                         foreign_amount   = er_entity-total_sales_amount
                         foreign_currency = er_entity-transaction_currency
                         local_currency   = er_entity-loc_curr
                       IMPORTING
                         exchange_rate    = lv_exchange_rate_ar
                         local_amount     = lv_local_amount_ar
                       EXCEPTIONS
                         no_rate_found    = 1
                         overflow         = 2
                         no_factors_found = 3
                         no_spread_found  = 4
                         derived_2_times  = 5
                         OTHERS           = 6.
                    IF sy-subrc <> 0.
*      Implement suitable error handling here
                    ENDIF.
                    er_entity-total_sales_amount_loccurr = lv_local_amount_ar.
                    CLEAR: lv_local_amount_ar, lv_exchange_rate_ar.
                 ENDIF.
                 IF er_entity-total_wth IS NOT INITIAL.
                 CALL FUNCTION 'CONVERT_TO_LOCAL_CURRENCY'
                       EXPORTING
                         date             = er_entity-billing_document_date
                         foreign_amount   = er_entity-total_wth
                         foreign_currency = er_entity-transaction_currency
                         local_currency   = er_entity-loc_curr
                       IMPORTING
                         exchange_rate    = lv_exchange_rate_ar
                         local_amount     = lv_local_amount_ar
                       EXCEPTIONS
                         no_rate_found    = 1
                         overflow         = 2
                         no_factors_found = 3
                         no_spread_found  = 4
                         derived_2_times  = 5
                         OTHERS           = 6.
                    IF sy-subrc <> 0.
*      Implement suitable error handling here
                    ENDIF.
                    er_entity-total_wth_loccur = lv_local_amount_ar.
                    CLEAR: lv_local_amount_ar, lv_exchange_rate_ar.
                 ENDIF.
               ELSE.
                 er_entity-total_sales_amount_loccurr = er_entity-total_sales_amount.
                 er_entity-total_discount_loccurr = er_entity-total_discount.
                 er_entity-total_other_charges_loccurr = er_entity-total_other_charges.
                 er_entity-total_wth_loccur = er_entity-total_wth.
               ENDIF.
      ENDIF.
      ENDIF.
     IF  ms_billing_document-landtx = lc_country_eg.
       er_entity-total_gross_amount_locurr = er_entity-total_gross_amount_locurr
                                                          - er_entity-total_wth_loccur.
       er_entity-total_gross_amount = er_entity-total_gross_amount - er_entity-total_wth.
       CALL FUNCTION 'SPELL_AMOUNT'
           EXPORTING
             amount    = er_entity-total_gross_amount_locurr
             currency  = er_entity-loc_curr
*            FILLER    = ' '
             language  = sy-langu
           IMPORTING
             in_words  = lt_words
           EXCEPTIONS
             not_found = 1
             too_large = 2
             OTHERS    = 3.
       CLEAR lv_words.
       IF sy-langu = 'A'.
         CONCATENATE lt_words-word lv_ktext lt_words-decword  lo_curr_eg INTO lv_words SEPARATED BY ' '.
       ELSE.
         CONCATENATE lt_words-word lv_ktext lt_words-decword  lc_curr_eg INTO lv_words SEPARATED BY ' '.
       ENDIF.
        TRANSLATE lv_words TO UPPER CASE.
        er_entity-total_amount_in_words = lv_words.
     ENDIF.

     IF  ms_billing_document-landtx = lc_country_sa OR
         ms_billing_document-landtx = lc_country_eg.
      "Fetch the QR code and UUID Details
      "--------------------------Check for E-documnet table
      DATA: ls_dd02v_edo_ar  TYPE dd02v,
            ls_ddobjname_ar  TYPE DDOBJNAME.
      IF ms_billing_document-landtx = lc_country_sa.
         ls_ddobjname_ar = 'EDOSAINV'.
      ELSEIF ms_billing_document-landtx = lc_country_eg.
         ls_ddobjname_ar = 'EDOEGINV'.
      ENDIF.
          CALL FUNCTION 'DDIF_TABL_GET'
            EXPORTING
              name          = ls_ddobjname_ar       " Name of the Table to be Read
              state         = 'A'              " Read Status of the Table
            IMPORTING
              dd02v_wa      = ls_dd02v_edo_ar     " Table Header
            EXCEPTIONS                         ##FM_SUBRC_OK
              illegal_input = 1                " Value not Allowed for Parameter
              OTHERS        = 2.
      IF ls_dd02v_edo_ar-tabname IS NOT INITIAL.

       DATA: lv_vbeln_vf TYPE vbeln_vf,
             lv_uuid TYPE EDOC_SA_UUID.
       DATA: lv_source_key TYPE edoc_source_key,
             lv_edoc_guid TYPE edoc_guid,
             lv_proc_status TYPE char10,
             lv_status TYPE CHAR30,
             lv_qr_code_x TYPE edoc_sa_xstring,
             lv_qr_code TYPE string,
             lv_bitmap TYPE xstring.
       lv_vbeln_vf = ms_billing_document-vbeln.
       cl_edoc_source_sd_invoice=>pack_key(
              EXPORTING iv_vbeln = lv_vbeln_vf
              IMPORTING ev_key = lv_source_key ).
       SELECT SINGLE edoc_guid PROC_STATUS FROM edocument INTO ( lv_edoc_guid, lv_proc_status )
                                             WHERE source_key = lv_source_key AND
                                                   proc_status <> 'CREATED'.  "#EC CI_NOORDER  "#EC CI_ALL_FIELDS_NEEDED
       IF ms_billing_document-landtx = lc_country_sa.
         "GetQRCodeDatafromKSASpecificDatabaseTableusingeDocumentGUID
         SELECT SINGLE UUID qr_code FROM edosainv INTO (lv_uuid, lv_qr_code_x)
                                    WHERE edoc_guid = lv_edoc_guid.
       ELSEIF ms_billing_document-landtx = lc_country_eg.
          SELECT SINGLE UUID FROM edoeginv INTO lv_uuid WHERE edoc_guid = lv_edoc_guid.  "#EC CI_NOORDER  "#EC CI_ALL_FIELDS_NEEDED
       ENDIF.
       SELECT SINGLE DESCRIPTION FROM EDOPROCSTATT INTO lv_status
                                    WHERE SPRAS = sy-langu AND PROCESS = 'SASIINV' AND
                                          PROC_STATUS = lv_proc_status.  "#EC CI_NOORDER  "#EC CI_ALL_FIELDS_NEEDED
         er_entity-uuid = lv_uuid.
         er_entity-status = lv_status.
       IF lv_qr_code_x IS NOT INITIAL.
       lv_qr_code = cl_http_utility=>if_http_utility~encode_x_base64(
                                                     unencoded = lv_qr_code_x ).
       "Convert to BMP formatted QRCode
       cl_rstx_barcode_renderer=>qr_code(
                          EXPORTING
                            i_module_size      = '6'
                            i_mode             = 'U'
                            i_error_correction = 'M'
                            i_barcode_text     = lv_qr_code
                          IMPORTING
                            e_bitmap           = lv_bitmap ).

       er_entity-qrcode_bitmap = lv_bitmap.
       ENDIF.
      ENDIF.
     ENDIF.

    "" Great Britain CE-2002

    IF  ms_billing_document-landtx = lc_country_gb.
*   SELECT single UKURS into er_entity-exchange_rate FROM tcurr where GDATU <= er_entity-BILLING_DOCUMENT_DATE and FCURR = 'EUR' and TCURR = 'GBP' and KURST = 'M'.
*     If sy-subrc = 0.
*       endif.
      DATA: lv_gjahr         TYPE gjahr,
            lv_local_amount  TYPE kwert,
            lv_exchange_rate TYPE string.
      DATA : lv_brtwr TYPE brtwr_lf.
      CONSTANTS : lc_curr      TYPE waerl VALUE 'GBP',
                  lc_rate_type TYPE kurst_curr VALUE 'M'.
      CLEAR : lv_fkdat, lv_vatdate.
      IF er_entity-transaction_currency NE lc_curr.
*        SELECT SINGLE gjahr fkdat FROM vbrk
*                   INTO (lv_gjahr, lv_fkdat)
*                   WHERE vbeln = ms_billing_document-vbeln.
*
*        SELECT SINGLE vatdate FROM bkpf
*                 INTO lv_vatdate
*                 WHERE bukrs = ms_billing_document-bukrs
*                 AND gjahr = lv_gjahr
*                 AND xblnr = ms_billing_document-vbeln
*                 AND blart = 'RV'.

        IF er_entity-tax_amount IS NOT INITIAL.
          CALL FUNCTION 'CONVERT_TO_LOCAL_CURRENCY'
            EXPORTING
              date             = er_entity-billing_document_date
              foreign_amount   = er_entity-tax_amount
              foreign_currency = er_entity-transaction_currency
              local_currency   = lc_curr
            IMPORTING
              local_amount     = lv_local_amount
              exchange_rate    = lv_exchange_rate
            EXCEPTIONS
              no_rate_found    = 1
              overflow         = 2
              no_factors_found = 3
              no_spread_found  = 4
              derived_2_times  = 5
              OTHERS           = 6.
        ENDIF.
        er_entity-condition_amount_loc_curr = lv_local_amount .
        CLEAR: lv_local_amount, lv_exchange_rate.

        IF er_entity-total_net_amount IS NOT INITIAL.
          CALL FUNCTION 'CONVERT_TO_LOCAL_CURRENCY'
            EXPORTING
              date             = er_entity-billing_document_date
              foreign_amount   = er_entity-total_net_amount
              foreign_currency = er_entity-transaction_currency
              local_currency   = lc_curr
            IMPORTING
              local_amount     = lv_local_amount
              exchange_rate    = lv_exchange_rate
            EXCEPTIONS
              no_rate_found    = 1
              overflow         = 2
              no_factors_found = 3
              no_spread_found  = 4
              derived_2_times  = 5
              OTHERS           = 6.
        ENDIF.
        er_entity-condition_base_value_loc_curr = lv_local_amount .
        er_entity-loc_curr = lc_curr.
        er_entity-exchange_rate = lv_exchange_rate.
      ENDIF.
    ENDIF.

    IF  ms_billing_document-landtx = lc_country_pl.
*** As per poland current recurement if total gross amount is more then or equal to 15000 PLN,plant and company code should be
*** in poland country code and material is maintained under material control code, then the bill is applicable for vat split relevant

      DATA:ls_plant            TYPE werks,
           lv_split_relevant   TYPE flag,
           lv_mpp_flag         TYPE flag,
           ls_billing_doc_item TYPE sdbil_odata_f_bd_item_std_s.

      set_billing_document_item( iv_billing_document = ms_billing_document-vbeln ). " Set billing document item data

      cl_glo_pl_utilities=>check_mpp_active(        " MPP Check
        EXPORTING
          iv_vbeln    =   ms_billing_document-vbeln   " Sales and Distribution Document Number
        CHANGING
          cv_mpp_flag =   lv_mpp_flag               " Single-Character Flag
      ).

      TEST-SEAM ts_flag.
      END-TEST-SEAM.
****  MPP Active Condition check
      IF mt_billing_document_item IS NOT INITIAL AND lv_mpp_flag EQ 'X'.
        LOOP AT mt_billing_document_item INTO ls_billing_doc_item.
**** checking country and plant are belongs to poland or not
          ls_plant = ls_billing_doc_item-plant.
          cl_glo_pl_split_utility=>plant_country_check(
            EXPORTING
              iv_plant          = ls_plant                         " Plant Table for National (Centrally Agreed) Contracts
              iv_company_code   = ms_billing_document-bukrs        " Company Code
            CHANGING
              cv_split_relevant = lv_split_relevant                " Split Payment Relevant
          ).

          TEST-SEAM ts_flag1.
          END-TEST-SEAM.

          IF lv_split_relevant EQ 'X'.                         " Value X set for VAT Split Indicator
            er_entity-indicator_vat_split = lv_mpp_flag.
            EXIT.
          ENDIF.              " End if lv_split_ind
        ENDLOOP.          " Loop End mt_billing_document_item
      ENDIF.             " End if MPP check
    ENDIF.  " End if poland check
  ENDMETHOD.


  METHOD isrprintdetails_get_entity.

    DATA ls_billing_document TYPE cl_fdp_v3_bd_form_utility=>ty_billing_document.

    ls_billing_document = ms_billing_document.

    TEST-SEAM skip.
    CALL METHOD cl_glo_log_form_utility=>read_isrprintdetails
      EXPORTING
        iv_bukrs = ls_billing_document-bukrs
        iv_vkorg = ls_billing_document-vkorg
        iv_fkwrt = ls_billing_document-netwr
        iv_vbeln = ls_billing_document-vbeln
        iv_kunrg = ls_billing_document-kunrg
        iv_waerk = ls_billing_document-waerk
      CHANGING
        cs_vbdre = er_entity.
     END-TEST-SEAM.

  ENDMETHOD.


  METHOD itemaftercorr_get_entityset.

    et_entityset = mt_item_after_correction.

  ENDMETHOD.


  METHOD ITEMDIFFERENCE_GET_ENTITYSET.

  et_entityset = mt_item_difference.

  ENDMETHOD.


  METHOD itempricaftcorr_get_entityset.

    DATA: ls_bil_doc_key TYPE /iwbep/s_mgw_name_value_pair,
          ls_item_key    TYPE /iwbep/s_mgw_name_value_pair.

    CLEAR: et_entityset,
           es_response_context.

* Sanity Check
    READ TABLE it_key_tab
         WITH KEY name = 'BillingDocument'
         INTO ls_bil_doc_key.

    ASSERT ms_billing_document-vbeln = ls_bil_doc_key-value.

* Item
    READ TABLE it_key_tab
         WITH KEY name = 'BillingDocumentItem'
         INTO ls_item_key.

* Get Item Price Conditions for corrected entries
    READ TABLE mt_item_pricing_aftercorr
         WITH KEY billing_document      = ms_billing_document-vbeln
                        billing_document_item = CONV #( ls_item_key-value )
         TRANSPORTING NO FIELDS.

    LOOP AT mt_item_pricing_aftercorr
         REFERENCE INTO DATA(lr_item_pricing_aftercorr)
         FROM sy-tabix.

      IF lr_item_pricing_aftercorr->billing_document_item <> ls_item_key-value.
        EXIT. "<<<
      ENDIF.

      INSERT lr_item_pricing_aftercorr->* INTO TABLE et_entityset.
    ENDLOOP.

  ENDMETHOD.


  METHOD itempriceconditi_get_entityset.

    CONSTANTS : lc_country_pl TYPE string VALUE 'PL'.

    FIELD-SYMBOLS: <fs_tab_entityset> LIKE LINE OF et_entityset.


    TRY.
        CALL METHOD super->itempriceconditi_get_entityset
          EXPORTING
            iv_entity_name           = iv_entity_name
            iv_entity_set_name       = iv_entity_set_name
            iv_source_name           = iv_source_name
            it_filter_select_options = it_filter_select_options
            is_paging                = is_paging
            it_key_tab               = it_key_tab
            it_navigation_path       = it_navigation_path
            it_order                 = it_order
            iv_filter_string         = iv_filter_string
            iv_search_string         = iv_search_string
            io_tech_request_context  = io_tech_request_context
          IMPORTING
            et_entityset             = et_entityset
            es_response_context      = es_response_context.
      CATCH /iwbep/cx_mgw_busi_exception .
      CATCH /iwbep/cx_mgw_tech_exception .
    ENDTRY.

     TEST-SEAM ts_amt.
     END-TEST-SEAM.
*    IF ms_billing_document-landtx = lc_country_pl      " Poland
*             AND ms_billing_document-vbtyp EQ 'P'.     " Correction Invoice - Debit Scenario
*
*      LOOP AT et_entityset ASSIGNING <fs_tab_entityset>.
*
*        IF <fs_tab_entityset>-condition_amount <> 0.
*          <fs_tab_entityset>-condition_amount = <fs_tab_entityset>-condition_amount * -1.  "Reverse the sign
*        ENDIF.
*
*      ENDLOOP.
*
*    ENDIF.

    IF ms_billing_document-landtx = lc_country_pl.      " Poland
      IF mv_correction_indicator <> 'X'  AND ms_billing_document-vbtyp EQ 'P'.     " Correction Invoice - Debit Scenario
        LOOP AT et_entityset ASSIGNING <fs_tab_entityset>.
          IF <fs_tab_entityset>-condition_amount <> 0.
            <fs_tab_entityset>-condition_amount = <fs_tab_entityset>-condition_amount * -1.  "Reverse the sign
          ENDIF.
        ENDLOOP.
      ENDIF.

      If mv_correction_indicator = 'X' AND ( ms_billing_document-vbtyp = 'O' or ms_billing_document-vbtyp = '6'). "differential Invoice - credit scenario
        LOOP AT et_entityset ASSIGNING <fs_tab_entityset>.
          IF <fs_tab_entityset>-condition_amount <> 0.
            <fs_tab_entityset>-condition_amount = <fs_tab_entityset>-condition_amount * -1.  "Reverse the sign
          ENDIF.
        ENDLOOP.
      ENDIF.
    ENDIF.


  ENDMETHOD.


  METHOD itempricingdiff_get_entityset.

    DATA: ls_bil_doc_key TYPE /iwbep/s_mgw_name_value_pair,
          ls_item_key    TYPE /iwbep/s_mgw_name_value_pair.

    CLEAR: et_entityset,
           es_response_context.

* Sanity Check
    READ TABLE it_key_tab
         WITH KEY name = 'BillingDocument'
         INTO ls_bil_doc_key.

    ASSERT ms_billing_document-vbeln = ls_bil_doc_key-value.

* Item
    READ TABLE it_key_tab
         WITH KEY name = 'BillingDocumentItem'
         INTO ls_item_key.

* Get Item Price Conditions Difference
    READ TABLE mt_item_pricing_difference
         WITH KEY billing_document      = ms_billing_document-vbeln
                        billing_document_item = CONV #( ls_item_key-value )
         TRANSPORTING NO FIELDS.

    LOOP AT mt_item_pricing_difference
         REFERENCE INTO DATA(lr_item_pricing_difference)
         FROM sy-tabix.

      IF lr_item_pricing_difference->billing_document_item <> ls_item_key-value.
        EXIT. "<<<
      ENDIF.

      INSERT lr_item_pricing_difference->* INTO TABLE et_entityset.
    ENDLOOP.

  ENDMETHOD.


  METHOD legallyrequiredt_get_entityset.

    CONSTANTS:lc_country_it    TYPE char2 VALUE 'IT'. "1811 HFC6

    DATA: wa_entity LIKE LINE OF et_entityset.
    DATA: ls_prcd TYPE prcd_elements,
          lc_lcit TYPE string VALUE 'LCIT'.



    TRY.
        CALL METHOD super->legallyrequiredt_get_entityset
          EXPORTING
            iv_entity_name           = iv_entity_name
            iv_entity_set_name       = iv_entity_set_name
            iv_source_name           = iv_source_name
            it_filter_select_options = it_filter_select_options
            is_paging                = is_paging
            it_key_tab               = it_key_tab
            it_navigation_path       = it_navigation_path
            it_order                 = it_order
            iv_filter_string         = iv_filter_string
            iv_search_string         = iv_search_string
            io_tech_request_context  = io_tech_request_context
          IMPORTING
            et_entityset             = et_entityset
            es_response_context      = es_response_context.


      CATCH /iwbep/cx_mgw_busi_exception .
      CATCH /iwbep/cx_mgw_tech_exception .
    ENDTRY.

    TEST-SEAM et_set.
    END-TEST-SEAM.

    CASE ms_billing_document-landtx.
      WHEN lc_country_it.

        SELECT SINGLE * FROM prcd_elements INTO ls_prcd WHERE knumv = ms_billing_document-knumv  "#EC CI_ALL_FIELDS_NEEDED
                                                          AND kschl = lc_lcit.
        IF sy-subrc EQ 0 AND ls_prcd-kinak <> ''.
          LOOP AT et_entityset INTO wa_entity.
            IF wa_entity-tax_code EQ ls_prcd-mwsk1.
              wa_entity-legally_required_text = ''.
              MODIFY et_entityset FROM wa_entity.
            ENDIF.
          ENDLOOP.
        ENDIF.

    ENDCASE.

  ENDMETHOD.


  METHOD opendownpayt_get_entity.
    DATA: lv_gross_amt TYPE netwr,
          lv_net_amt   TYPE netwr,
          lv_tax_amt   TYPE netwr.

    CLEAR: lv_gross_amt,lv_net_amt, lv_tax_amt.


    lv_net_amt = ms_billing_document-netwr - ms_cleared_downpayment_ovw-downpaymentnetamount.
    lv_tax_amt = ms_billing_document-mwsbk - ms_cleared_downpayment_ovw-downpaymenttaxamount.
    lv_gross_amt = lv_net_amt + lv_tax_amt.

    er_entity-downpaymentgrossamount = lv_gross_amt.
    er_entity-downpaymentnetamount = lv_net_amt.
    er_entity-downpaymenttaxamount = lv_tax_amt.

    CLEAR: ms_cleared_downpayment_ovw.

  ENDMETHOD.


  METHOD partyaddressset_get_entity.

    DATA: lc_country_in  TYPE string VALUE 'IN',
          lc_country_ae  TYPE string VALUE 'AE',
          lc_country_om  TYPE string VALUE 'OM',
          lc_country_sa  TYPE string VALUE 'SA',
          lc_country_eg  TYPE string VALUE 'EG',
          lv_region_name TYPE bezei,
          ls_adrc        TYPE adrc.
    DATA:
      lo_data_buffer TYPE REF TO cl_fdp_v3_data_buffer,
      ls_partner     TYPE sdbil_odata_f_party_s.

    FIELD-SYMBOLS: <ls_entity_party_address> TYPE sdbil_odata_f_party_s.

    CLEAR: lv_region_name,
           ls_adrc.


    CLEAR: er_entity,
           es_response_context.


    mv_language = get_language( ).
    mv_sender_country = get_sender_country( ).
    lo_data_buffer = cl_fdp_v3_bd_form_utility=>get_data_buffer( ).

    ls_partner-partner_function = 'RE'.

    READ TABLE lo_data_buffer->mt_partners WITH KEY parvw = ls_partner-partner_function REFERENCE INTO DATA(lr_partner).
    IF lr_partner IS NOT INITIAL.
      ls_partner-billing_document = lr_partner->vbeln.
      ls_partner-partner_function = lr_partner->parvw.
      ls_partner-partner          = lr_partner->kunnr.
      ls_partner-address_id       = lr_partner->adrnr.
      ls_partner-address_type     = lr_partner->addr_type.

      ASSIGN er_entity TO  <ls_entity_party_address>.
      <ls_entity_party_address> = ls_partner.
    ENDIF.

    IF <ls_entity_party_address> IS ASSIGNED.
      <ls_entity_party_address>-person   = cl_fdp_v3_bd_form_utility=>get_person_number(
                                              iv_vbeln = <ls_entity_party_address>-billing_document
                                              iv_parvw = 'BP'
                                              iv_posnr = <ls_entity_party_address>-billing_document_item ).
    ENDIF.

    TEST-SEAM skip_cl.
*     Name, Additional Name, Address Type, Address Line 1 - 8
    cl_fdp_v3_bd_form_utility=>get_address_in_printform(
      EXPORTING
        iv_language        = mv_language
        iv_sender_country  = mv_sender_country
        iv_kunnr           = <ls_entity_party_address>-partner
        iv_adrnp           = <ls_entity_party_address>-person
        iv_adrnr           = <ls_entity_party_address>-address_id
        iv_address_type    = <ls_entity_party_address>-address_type
      IMPORTING
        ev_full_name       = <ls_entity_party_address>-full_name
        ev_address_type    = <ls_entity_party_address>-address_type
        ev_address_line1   = <ls_entity_party_address>-address_line_1
        ev_address_line2   = <ls_entity_party_address>-address_line_2
        ev_address_line3   = <ls_entity_party_address>-address_line_3
        ev_address_line4   = <ls_entity_party_address>-address_line_4
        ev_address_line5   = <ls_entity_party_address>-address_line_5
        ev_address_line6   = <ls_entity_party_address>-address_line_6
        ev_address_line7   = <ls_entity_party_address>-address_line_7
        ev_address_line8   = <ls_entity_party_address>-address_line_8
    ).
    END-TEST-SEAM.

    IF ms_billing_document-landtx = lc_country_in.

      SELECT SINGLE * FROM adrc              "#EC CI_ALL_FIELDS_NEEDED                        " Fetching region
                      INTO ls_adrc
                       WHERE addrnumber = er_entity-address_id.
      IF sy-subrc = 0.
        SELECT SINGLE bezei FROM t005u                              " Fetching region name
                       INTO  lv_region_name
                       WHERE spras EQ sy-langu AND
                             land1 EQ ls_adrc-country AND
                             bland EQ ls_adrc-region.
        IF sy-subrc = 0.
          er_entity-region_name = lv_region_name.                   " Region Name
          CLEAR: lv_region_name.
        ENDIF.

        er_entity-region = ls_adrc-region.                          " Region
        CLEAR: ls_adrc.
      ENDIF.

    ENDIF.
***1908 HFC02 UAE/KSA Customer Invoice
    IF ms_billing_document-landtx = lc_country_ae OR
       ms_billing_document-landtx = lc_country_sa OR
       ms_billing_document-landtx = lc_country_om OR
       ms_billing_document-landtx = lc_country_EG.

      SELECT SINGLE cityname,streetname,faxnumber,telephonenumber1,country,customerfullname FROM i_customer INTO @DATA(lv_communication) WHERE customer = @er_entity-partner.
      er_entity-city             = lv_communication-cityname.
      er_entity-street           = lv_communication-streetname.
      er_entity-fax_number       = lv_communication-faxnumber.
      er_entity-telephone_number = lv_communication-telephonenumber1.
      er_entity-full_name        = lv_communication-customerfullname.

      SELECT SINGLE countryname FROM i_countrytext INTO @DATA(lv_country) WHERE country = @lv_communication-country AND language = @sy-langu.
      er_entity-countryname = lv_country.

      SELECT SINGLE * FROM adrc                                   "#EC CI_ALL_FIELDS_NEEDED
                      INTO ls_adrc
                       WHERE addrnumber = er_entity-address_id.   "#EC CI_NOORDER   "#EC CI_ALL_FIELDS_NEEDED
      IF sy-subrc = 0.
         er_entity-street = ls_adrc-Street.
         CONCATENATE ls_adrc-str_suppl1 ls_adrc-str_suppl2 ls_adrc-str_suppl3 INTO er_entity-address_line_1 SEPARATED BY space.
         er_entity-address_line_2 = ls_adrc-house_num1.
         er_entity-address_line_3 = ls_adrc-house_num2.
         er_entity-postal_code = ls_adrc-post_code1.
         er_entity-region = ls_adrc-region.
      ENDIF.
      SELECT SINGLE BEZEI FROM T005U INTO er_entity-region_name WHERE SPRAS = sy-langu AND
                                           LAND1 = ms_billing_document-landtx AND
                                           BLAND = ls_adrc-region.

    ENDIF.

  ENDMETHOD.


  method PRICECONDITIONSE_GET_ENTITYSET.

    CONSTANTS : lc_country_pl TYPE string VALUE 'PL'.

    FIELD-SYMBOLS: <fs_tab_entityset> LIKE LINE OF et_entityset.

    DATA: lv_gjahr         TYPE gjahr,
          lv_fkdat         TYPE fkdat,
          lv_vatdate       TYPE vatdate,
          lv_local_amount  TYPE kwert,
          lv_exchange_rate TYPE string.
    TRY.
        CALL METHOD SUPER->PRICECONDITIONSE_GET_ENTITYSET
          EXPORTING
            IV_ENTITY_NAME           = IV_ENTITY_NAME
            IV_ENTITY_SET_NAME       = IV_ENTITY_SET_NAME
            IV_SOURCE_NAME           = IV_SOURCE_NAME
            IT_FILTER_SELECT_OPTIONS = IT_FILTER_SELECT_OPTIONS
            IS_PAGING                = IS_PAGING
            IT_KEY_TAB               = IT_KEY_TAB
            IT_NAVIGATION_PATH       = IT_NAVIGATION_PATH
            IT_ORDER                 = IT_ORDER
            IV_FILTER_STRING         = IV_FILTER_STRING
            IV_SEARCH_STRING         = IV_SEARCH_STRING
            IO_TECH_REQUEST_CONTEXT  = IO_TECH_REQUEST_CONTEXT
          IMPORTING
            ET_ENTITYSET             = ET_ENTITYSET
            ES_RESPONSE_CONTEXT      = ES_RESPONSE_CONTEXT.
      CATCH /IWBEP/CX_MGW_BUSI_EXCEPTION .
      CATCH /IWBEP/CX_MGW_TECH_EXCEPTION .
    ENDTRY.

    TEST-SEAM ts_1.
    END-TEST-SEAM.

    " To convert condition amount into local currency based on BKPF-VATDATE.
*    If ms_billing_document-landtx = lc_country_pl.
*
*
*      SELECT SINGLE gjahr fkdat FROM vbrk
*                 INTO (lv_gjahr, lv_fkdat)
*                 WHERE vbeln = ms_billing_document-vbeln.
*
*      SELECT SINGLE vatdate FROM bkpf
*               INTO lv_vatdate
*               WHERE bukrs = ms_billing_document-bukrs
*               AND gjahr = lv_gjahr
*               AND xblnr = ms_billing_document-vbeln
*               AND blart = 'RV'.
*
*    IF lv_fkdat <> lv_vatdate.
*        LOOP AT et_entityset ASSIGNING <fs_tab_entityset>.
*
*          IF <fs_tab_entityset>-CONDITION_AMOUNT IS NOT INITIAL.
*            CALL FUNCTION 'CONVERT_TO_LOCAL_CURRENCY'
*              EXPORTING
*                date             = lv_vatdate
*                foreign_amount   = <fs_tab_entityset>-condition_amount
*                foreign_currency = <fs_tab_entityset>-document_currency
*                local_currency   = <fs_tab_entityset>-loc_curr
*              IMPORTING
*                local_amount     = lv_local_amount
*                exchange_rate    = lv_exchange_rate
*              EXCEPTIONS
*                no_rate_found    = 1
*                overflow         = 2
*                no_factors_found = 3
*                no_spread_found  = 4
*                derived_2_times  = 5
*                OTHERS           = 6.
*          ENDIF.
*          <fs_tab_entityset>-condition_amount_loc_curr = lv_local_amount .
*        ENDLOOP.
*      endif.
*    ENDIF.

*** Poland Correction Invoice Form

    IF ms_billing_document-landtx = lc_country_pl
             AND ms_billing_document-vbtyp EQ 'O'.     " Correction Invoice

      LOOP AT et_entityset ASSIGNING <fs_tab_entityset>.

        IF <fs_tab_entityset>-condition_amount <> 0.
          <fs_tab_entityset>-condition_amount = <fs_tab_entityset>-condition_amount * -1.  "Reverse the sign
        ENDIF.

      ENDLOOP.

    ENDIF.



  endmethod.


  method SEPASET_GET_ENTITY.
 TRY.
     CALL METHOD super->sepaset_get_entity
       EXPORTING
         iv_entity_name          = iv_entity_name
         iv_entity_set_name      = iv_entity_set_name
         iv_source_name          = iv_source_name
         it_key_tab              = it_key_tab
         io_request_object       = io_request_object
         io_tech_request_context = io_tech_request_context
         it_navigation_path      = it_navigation_path
       IMPORTING
         er_entity               = er_entity
         es_response_context     = es_response_context.
   CATCH /iwbep/cx_mgw_busi_exception.
   CATCH /iwbep/cx_mgw_tech_exception.
 ENDTRY.
    DATA : lc_country_in TYPE string VALUE 'IN',
           lv_banka      TYPE banka,
           lv_bic        TYPE swift,
           lv_kunnr      TYPE kunnr,
           lv_bankl      TYPE bankk.
    IF ms_billing_document-landtx = lc_country_in.
      CLEAR : lv_kunnr, lv_bankl,lv_bic,lv_banka.
      IF ms_billing_document-kunrg IS NOT INITIAL .
        lv_kunnr = ms_billing_document-kunrg.
        SELECT SINGLE bankl FROM knbk  INTO lv_bankl WHERE kunnr = lv_kunnr
                                              AND   banks = lc_country_in.
        IF sy-subrc IS INITIAL.
          SELECT SINGLE banka swift FROM bnka INTO (lv_banka , lv_bic)
                                    WHERE banks = lc_country_in
                                    AND bankl =  lv_bankl.
          IF sy-subrc IS INITIAL.
            er_entity-bank_name = lv_banka.
            er_entity-bic_number = lv_bic.

          ENDIF.

        ENDIF.
      ENDIF.
    ENDIF.
  endmethod.


  METHOD serialnumber_get_entityset.

    DATA: ls_bil_doc_key TYPE /iwbep/s_mgw_name_value_pair,
          ls_item_key    TYPE /iwbep/s_mgw_name_value_pair,
          ls_entityset   LIKE LINE OF et_entityset,
          lo_data_buffer TYPE REF TO cl_fdp_v3_data_buffer,
          ls_item_buffer TYPE vbdpr.

    DATA: ls_item_delivery_ref   LIKE LINE OF mt_item_delivery_ref,
          ls_item_salesorder_ref LIKE LINE OF mt_item_salesorder_ref.

    FIELD-SYMBOLS: <fs_serial_numbers> LIKE LINE OF mt_serial_numbers.

    CLEAR: et_entityset,
           es_response_context.

* Sanity Check
    READ TABLE it_key_tab
         WITH KEY name = 'BillingDocument'
         INTO ls_bil_doc_key.

    lo_data_buffer = cl_fdp_v3_bd_form_utility=>get_data_buffer( ).
    ASSERT lo_data_buffer->ms_header-vbeln = ls_bil_doc_key-value.

* Item
    READ TABLE it_key_tab
         WITH KEY name = 'BillingDocumentItem'
         INTO ls_item_key.

    ls_entityset-billing_document = lo_data_buffer->ms_header-vbeln.
    ls_entityset-billing_document_item = ls_item_key-value.

    IF mt_serial_numbers IS INITIAL.
      fill_serial_numbers( ).
    ENDIF.

    READ TABLE lo_data_buffer->mt_item WITH KEY vbeln = lo_data_buffer->ms_header-vbeln posnr = ls_item_key-value INTO ls_item_buffer.
    IF ls_item_buffer-vbeln_vl IS NOT INITIAL.
      ls_item_delivery_ref-vbeln_vl = ls_item_buffer-vbeln_vl.
      ls_item_delivery_ref-posnr_vl = ls_item_buffer-posnr_vl.
    ELSE.
      ls_item_salesorder_ref-aubel = ls_item_buffer-aubel.
      ls_item_salesorder_ref-aupos = ls_item_buffer-aupos.
    ENDIF.

    IF ls_item_delivery_ref IS NOT INITIAL.
      LOOP AT mt_serial_numbers ASSIGNING <fs_serial_numbers> WHERE lief_nr = ls_item_delivery_ref-vbeln_vl AND posnr = ls_item_delivery_ref-posnr_vl.
        ls_entityset-serial_number = <fs_serial_numbers>-sernr.
        INSERT ls_entityset INTO TABLE et_entityset.
      ENDLOOP.
    ELSE.
      LOOP AT mt_serial_numbers ASSIGNING <fs_serial_numbers> WHERE sdaufnr = ls_item_salesorder_ref-aubel AND posnr = ls_item_salesorder_ref-aupos.
        ls_entityset-serial_number = <fs_serial_numbers>-sernr.
        INSERT ls_entityset INTO TABLE et_entityset.
      ENDLOOP.
    ENDIF.
  ENDMETHOD.


  METHOD servicerecipient_get_entity.

    DATA: lc_country_in  TYPE string VALUE 'IN',
          lv_region_name TYPE bezei,
          ls_adrc        TYPE adrc,
          lv_j_1ipanno TYPE j_1ipanno.

    CLEAR: lv_region_name,
           ls_adrc.

    TRY.
        CALL METHOD super->servicerecipient_get_entity
          EXPORTING
            iv_entity_name          = iv_entity_name
            iv_entity_set_name      = iv_entity_set_name
            iv_source_name          = iv_source_name
            it_key_tab              = it_key_tab
            io_request_object       = io_request_object
            io_tech_request_context = io_tech_request_context
            it_navigation_path      = it_navigation_path
          IMPORTING
            er_entity               = er_entity
            es_response_context     = es_response_context.
      CATCH /iwbep/cx_mgw_busi_exception .
      CATCH /iwbep/cx_mgw_tech_exception .
    ENDTRY.

    TEST-SEAM fill_er5.
    END-TEST-SEAM.

    IF ms_billing_document-landtx = lc_country_in.

      SELECT SINGLE * FROM adrc                            "#EC CI_ALL_FIELDS_NEEDED          " Fetching region
                      INTO ls_adrc
                       WHERE addrnumber = er_entity-address_id.
      IF sy-subrc = 0.
        SELECT SINGLE bezei FROM t005u                              " Fetching region name
                       INTO  lv_region_name
                       WHERE spras EQ sy-langu AND
                             land1 EQ ls_adrc-country AND
                             bland EQ ls_adrc-region.
        IF sy-subrc = 0.
          er_entity-region_name = lv_region_name.                   " Region Name
          CLEAR: lv_region_name.
        ENDIF.

        er_entity-region = ls_adrc-region.                          " Region
        CLEAR: ls_adrc.
      ENDIF.
      SELECT SINGLE j_1ipanno FROM kna1 INTO lv_j_1ipanno
                    WHERE kunnr = er_entity-partner.
      IF  sy-subrc IS INITIAL.
        er_entity-pan_no_company = lv_j_1ipanno.
      ENDIF.
    ENDIF.

  ENDMETHOD.


  method SET_BILLING_DOCUMENT_ITEM.
    DATA:ls_vbrp                  TYPE vbrp,
         lt_vbrp                  TYPE TABLE OF vbrp,
         ls_billing_document_item LIKE LINE OF mt_billing_document_item.

    SELECT vbeln, matnr, werks FROM vbrp INTO CORRESPONDING FIELDS OF TABLE @lt_vbrp WHERE vbeln = @iv_billing_document.

    IF lt_vbrp IS NOT INITIAL.
      LOOP AT lt_vbrp INTO ls_vbrp.
        ls_billing_document_item-billing_document = ls_vbrp-vbeln.
        ls_billing_document_item-product = ls_vbrp-matnr.
        ls_billing_document_item-plant = ls_vbrp-werks.
        APPEND ls_billing_document_item TO mt_billing_document_item.
        CLEAR:ls_billing_document_item, ls_vbrp.
      ENDLOOP.
    ENDIF.
  endmethod.


  method SUPPLIER_GET_ENTITY.

*--Data Declaration
    DATA : lv_plant       TYPE werks_d,
           lv_companycode TYPE bukrs,
           lv_branch      TYPE j_1bbranc_,
           lv_gstin       TYPE stcd3,
           ls_adrc        TYPE adrc,
           lv_state_desc  TYPE bezei,
           lv_cntry_desc  TYPE landx,
           ls_branch      TYPE j_1bbranch,
           ls_adrs        TYPE adrs_print.

    CLEAR: ls_adrc,
           ls_branch,
           ls_adrs.

  mv_language = get_language( ).
  mv_sender_country = get_sender_country( ).

  er_entity-company_code = ms_billing_document-bukrs.



* -- To Fetch supplier details
*-- Plant : Take plant details from the first item
    SELECT werks
      FROM vbrp                                        ##DB_FEATURE_MODE[TABLE_LEN_MAX1]
      INTO lv_plant
      WHERE     vbeln = ms_billing_document-vbeln
      ORDER BY posnr ASCENDING.
      EXIT. "<<<
    ENDSELECT.

* --Get the GSTIN
    CALL FUNCTION 'J_1IG_GET_PLANT_DETAILS'
      EXPORTING
        im_werks  = lv_plant
        im_bukrs  = ms_billing_document-bukrs
      IMPORTING
        ex_branch = lv_branch
        ex_gstin  = lv_gstin.

*--fetch the BUPLA Adress number
    SELECT SINGLE *
                  FROM j_1bbranch
                  INTO ls_branch
                  WHERE bukrs EQ ms_billing_document-bukrs AND
                        branch EQ lv_branch.

    TEST-SEAM ts_sub.
    END-TEST-SEAM.

    IF sy-subrc IS INITIAL.

       CALL FUNCTION 'ADDRESS_INTO_PRINTFORM'
            EXPORTING
              address_type        = '1'
              address_number      = ls_branch-adrnr
              receiver_language   = mv_language
              sender_country      = mv_sender_country
              number_of_lines     = 6
              street_has_priority = abap_false
            IMPORTING
              address_printform   = ls_adrs.

** AddressLine1 - AddressLine6
          er_entity-address_line_1 = ls_adrs-line0.
          er_entity-address_line_2 = ls_adrs-line1.
          er_entity-address_line_3 = ls_adrs-line2.
          er_entity-address_line_4 = ls_adrs-line3.
          er_entity-address_line_5 = ls_adrs-line4.
          er_entity-address_line_6 = ls_adrs-line5.



      SELECT SINGLE * FROM adrc      "#EC CI_ALL_FIELDS_NEEDED
                      INTO ls_adrc
                      WHERE addrnumber = ls_branch-adrnr.
      IF sy-subrc IS INITIAL.
*--state description
        SELECT SINGLE bezei FROM t005u
                     INTO lv_state_desc
                     WHERE spras = 'EN' AND
                           land1 = ls_adrc-country AND
                           bland = ls_adrc-region.
*--Country Description
        SELECT SINGLE landx FROM t005t
                     INTO lv_cntry_desc
                     WHERE spras EQ 'EN' AND
                           land1 EQ ls_adrc-country.

      ENDIF.
    ENDIF.


*--Moving the values to the corresponding properties of entity

er_entity-address_id   = ls_branch-adrnr.
er_entity-full_name    = ls_adrc-name_text.
er_entity-company_code = ms_billing_document-bukrs.
er_entity-region       = ls_adrc-region.
er_entity-region_name  = lv_state_desc.


  endmethod.


  METHOD taxationtermsset_get_entity.

    CONSTANTS: lc_country_ph TYPE string VALUE 'PH'.
    CONSTANTS: lc_country_ca TYPE string VALUE 'CA'.
    CONSTANTS: lc_country_id TYPE string VALUE 'ID'.
    CONSTANTS: lc_country_pl TYPE string VALUE 'PL'.
    CONSTANTS: lc_country_in TYPE string VALUE 'IN'.
    CONSTANTS: lc_country_cz TYPE string VALUE 'CZ'.
    CONSTANTS: lc_parvw_re TYPE string VALUE 'RE'.
    CONSTANTS: lc_parvw_we TYPE string VALUE 'WE'.
    CONSTANTS: lc_taxtype_ph TYPE string VALUE 'PH1'.
    CONSTANTS: lc_taxtype_id TYPE string VALUE 'ID1'.
    CONSTANTS: lc_taxtype_in TYPE string VALUE 'IN3'.
    CONSTANTS: lc_type TYPE bu_id_type VALUE 'FS0001'.
    CONSTANTS: lc_country_eg TYPE string VALUE 'EG'.

    DATA: ls_vbpa TYPE vbpa.
    DATA: lt_vbpa TYPE STANDARD TABLE OF vbpa.
    DATA: lt_taxnum TYPE TABLE OF dfkkbptaxnum.
    DATA: ls_taxnum TYPE dfkkbptaxnum.
    DATA: lv_partner TYPE bu_partner.
    DATA: lv_kunnr TYPE vbpa-kunnr.
    DATA: lv_xegld TYPE xegld.
    DATA: lv_stcd1 type vbpa3-stcd1.
    DATA: lv_parvw type vbpa3-parvw.
    DATA: lv_plant TYPE werks_d.
    DATA: lv_adrnr TYPE vbpa-adrnr.
    DATA: ls_customer_re TYPE cmd_bp_cust_gen_s.
    DATA: ls_customer_we TYPE cmd_bp_cust_gen_s.

    CLEAR: ls_vbpa,
           lv_plant.

    TRY.
        CALL METHOD super->taxationtermsset_get_entity
          EXPORTING
            iv_entity_name          = iv_entity_name
            iv_entity_set_name      = iv_entity_set_name
            iv_source_name          = iv_source_name
            it_key_tab              = it_key_tab
            io_request_object       = io_request_object
            io_tech_request_context = io_tech_request_context
            it_navigation_path      = it_navigation_path
          IMPORTING
            er_entity               = er_entity
            es_response_context     = es_response_context.
        TEST-SEAM ts_exc.
        END-TEST-SEAM.
      CATCH /iwbep/cx_mgw_busi_exception .
      CATCH /iwbep/cx_mgw_tech_exception .
    ENDTRY.

    TEST-SEAM fill_er3.
    END-TEST-SEAM.

    IF ms_billing_document IS INITIAL.

      CALL METHOD get_billing_document
        RECEIVING
          rs_billing_document = ms_billing_document.
    ENDIF.

*  Fill tax numbers to expose

    CALL FUNCTION 'SD_VBPA_READ_WITH_VBELN'
      EXPORTING
        i_vbeln          = er_entity-billing_document
      TABLES
        et_vbpa          = lt_vbpa
      EXCEPTIONS
        record_not_found = 1
        OTHERS           = 2.

    TEST-SEAM fill_vbpa.
    END-TEST-SEAM.
    IF sy-subrc <> 0.
* Implement suitable error handling here
    ELSE.
      READ TABLE lt_vbpa INTO ls_vbpa WITH KEY parvw = lc_parvw_re.
      IF sy-subrc = 0.
*      ls_vbpa = VALUE #( lt_vbpa[ parvw = lc_parvw_re ] ).
*      IF ls_vbpa IS NOT INITIAL.
*        CALL FUNCTION 'BUPA_TAX_SELECT_WITH_PARTNER'
*          EXPORTING
*            iv_partner     = ls_vbpa-kunnr
*            iv_addrnumber  = ls_vbpa-adrnr
*          TABLES
*            et_tax_numbers = lt_taxnum.

        CLEAR: ls_customer_re.
        DATA(lo_bp) = cl_glo_log_utilities=>get_instance( ).

        CALL METHOD lo_bp->get_customer_tax_details
          EXPORTING
            iv_customer     = ls_vbpa-kunnr
            iv_address      = ls_vbpa-adrnr
            iv_adr_ind      = ls_vbpa-adrda
            iv_bp_ref_adrnr = ls_vbpa-bp_ref_adrnr
            iv_stceg        = ls_vbpa-stceg
          receiving
            rs_customer     = ls_customer_re.

         er_entity-tax_number0 = ls_customer_re-customer-stceg.
         er_entity-tax_number1 = ls_customer_re-customer-stcd1.
         er_entity-tax_number2 = ls_customer_re-customer-stcd2.
         er_entity-tax_number3 = ls_customer_re-customer-stcd3.
         er_entity-tax_number4 = ls_customer_re-customer-stcd4.
         er_entity-tax_number5 = ls_customer_re-customer-stcd5.

        TEST-SEAM fill_tax.
        END-TEST-SEAM.

      ENDIF.
*
      READ TABLE lt_vbpa INTO ls_vbpa WITH KEY parvw = lc_parvw_we.
      IF sy-subrc = 0.
*        CLEAR ls_vbpa.
*        ls_vbpa = VALUE #( lt_vbpa[ parvw = lc_parvw_we ] ).
*        IF ls_vbpa IS NOT INITIAL.
        CLEAR: ls_customer_we.
        DATA(lo_bp1) = cl_glo_log_utilities=>get_instance( ).

        CALL METHOD lo_bp1->get_customer_tax_details
          EXPORTING
            iv_customer     = ls_vbpa-kunnr
            iv_address      = ls_vbpa-adrnr
            iv_adr_ind      = ls_vbpa-adrda
            iv_bp_ref_adrnr = ls_vbpa-bp_ref_adrnr
            iv_stceg        = ls_vbpa-stceg
          receiving
            rs_customer     = ls_customer_we.
      ENDIF.
    ENDIF.

* Czech republic specific
    IF ms_billing_document-landtx = lc_country_cz OR ms_billing_document-land1 = lc_country_cz.
****mapping customer IC number
      er_entity-cust_ic_num = er_entity-tax_number2.

****Company IC number for CZ is its VAT no. without leading 'CZ'
      IF er_entity-vat_reg_no_company IS NOT INITIAL.
        er_entity-supl_ic_num = er_entity-vat_reg_no_company.

        IF er_entity-supl_ic_num CP 'CZ*'.
          REPLACE ALL OCCURRENCES OF REGEX 'CZ' IN er_entity-supl_ic_num WITH ''.
        ENDIF.

      ENDIF.

    ENDIF.

    IF ms_billing_document-landtx = lc_country_ph.

*      READ TABLE lt_taxnum INTO ls_taxnum WITH KEY taxtype = lc_taxtype_ph.
*      IF ls_taxnum-taxnum IS NOT INITIAL.
*        er_entity-cust_tin_num = ls_taxnum-taxnum.
*      ELSE.
*        er_entity-cust_tin_num = ls_taxnum-taxnumxl.
*      ENDIF.
      IF ls_customer_re-customer-stcd1 IS NOT INITIAL AND ls_customer_re-customer-stcd1 CP 'PH*'.
        er_entity-cust_tin_num = ls_customer_re-customer-stcd1.
      ENDIF.

    ENDIF.

    IF ms_billing_document-landtx = lc_country_ca.
*** Determine Ship-to of first item in invoice
*      CLEAR:ls_vbpa,ls_customer.
*      READ TABLE lt_vbpa INTO ls_vbpa WITH KEY parvw = lc_parvw_we.
*      IF sy-subrc = 0.
**        SELECT SINGLE stcd3 INTO er_entity-pst_reg_num FROM kna1 WHERE kunnr = lv_kunnr.
*         "Multiple BP Address Adaptations
*         DATA(lo_bp1) = cl_glo_log_utilities=>get_instance( ).
*
*         CALL METHOD lo_bp1->get_customer_tax_details
*          EXPORTING
*            iv_customer     = ls_vbpa-kunnr
*            iv_address      = ls_vbpa-adrnr
*            iv_adr_ind      = ls_vbpa-adrda
*            iv_bp_ref_adrnr = ls_vbpa-bp_ref_adrnr
*            iv_stceg        = ls_vbpa-stceg
*          receiving
*            rs_customer     = ls_customer.

         er_entity-pst_reg_num = ls_customer_we-customer-stcd3.
*      ENDIF.
    ENDIF.

***   Indonesia
    IF ms_billing_document-landtx = lc_country_id.
*  Company Code NPWP Number
      SELECT SINGLE paval
              FROM t001z
              INTO er_entity-company_code_tin
              WHERE bukrs = ms_billing_document-bukrs
              AND   party = 'IDNPWP'.

*  Customer NPWP Number
       IF ls_customer_re-customer-stcd1 IS NOT INITIAL AND ls_customer_re-customer-stcd1 CP 'ID*'.
        er_entity-cust_tin_num = ls_customer_re-customer-stcd1.
       ENDIF.

*  Customer NIK Number
      SELECT SINGLE idnumber
              FROM but0id
              INTO er_entity-tax_number5
              WHERE partner = ls_vbpa-kunnr
              AND   type = lc_type.

    ENDIF.

*    Fill tax number ES1 if Spain customer else if EU customer fill tax number from master data
*    Fill  original tax number  if Poland customer else if EU customer fill tax number from master data
    IF ( ms_billing_document-landtx = 'ES' OR ms_billing_document-landtx = 'PL' )
       AND er_entity-vat_reg_no_bill_to IS INITIAL.

      IF ms_billing_document-land1 = 'ES' OR ms_billing_document-land1 = 'PL'.

        er_entity-vat_reg_no_bill_to = er_entity-tax_number1.

      ELSE.

        SELECT  SINGLE xegld INTO lv_xegld FROM t005 WHERE land1 = ms_billing_document-land1.
        IF lv_xegld = abap_true.
          er_entity-vat_reg_no_bill_to = er_entity-tax_number0.
        ENDIF.
      ENDIF.

      " To Fetch VAT Registration number for one time customer.
      IF ms_billing_document-land1 = 'PL' .
        IF er_entity-vat_reg_origin = 'C'.              "Sold-To Party
          lv_parvw = 'AG'.
        ELSEIF er_entity-vat_reg_origin = 'A'.          "Ship-To Party
          lv_parvw = 'WE' .
        ENDIF.
        TEST-SEAM ts_vb.
        END-TEST-SEAM.
        CLEAR ls_vbpa.
        READ TABLE lt_vbpa INTO ls_vbpa WITH KEY parvw = lv_parvw.
        If sy-subrc = 0 AND ls_vbpa-xcpdk = 'X'.
          "To Fetch VAT registration number for one time customer.
          SELECT SINGLE stcd1 FROM VBPA3 INTO lv_stcd1 WHERE  vbeln = ms_billing_document-vbeln_so AND
                                                              parvw = lv_parvw.

          IF lv_stcd1 IS NOT INITIAL.
            er_entity-vat_reg_no_bill_to = lv_stcd1.
          ENDIF.
        ENDIF.

      ENDIF.


    ENDIF.

* Poland Specific
*  If the customer is domestic (from Poland) , then company VAT registration number shall be printed without “PL” if PL is there at start.
    IF  ms_billing_document-landtx = lc_country_pl AND ms_billing_document-land1 = lc_country_pl.
      IF er_entity-vat_reg_no_company CP 'PL*'.
        REPLACE ALL OCCURRENCES OF REGEX 'PL' IN er_entity-vat_reg_no_company WITH ''.
      ENDIF.
      IF er_entity-vat_reg_no_bill_to CP 'PL*'.
        REPLACE ALL OCCURRENCES OF REGEX 'PL' IN er_entity-vat_reg_no_bill_to WITH ''.
      ENDIF.
    ENDIF.


* India
 IF ms_billing_document-landtx = lc_country_in.

*--To Fetch supplier details
*-- Plant : Take plant details from the first item
    SELECT werks
      FROM vbrp                                        ##DB_FEATURE_MODE[TABLE_LEN_MAX1]
      INTO lv_plant
      WHERE vbeln = ms_billing_document-vbeln
      ORDER BY posnr ASCENDING.
      EXIT. "<<<
    ENDSELECT.

* --Get the GSTIN
    CALL FUNCTION 'J_1IG_GET_PLANT_DETAILS'
      EXPORTING
        im_werks  = lv_plant
        im_bukrs  = ms_billing_document-bukrs
      IMPORTING
*        ex_branch = lv_branch
        ex_gstin  = er_entity-gstin.

*-- To Fetch Bill To Party GSTIN
*     CLEAR: ls_taxnum.
*     READ TABLE lt_taxnum INTO ls_taxnum WITH KEY taxtype = lc_taxtype_in.
*     IF sy-subrc = 0.
*       IF ls_taxnum-taxnum IS NOT INITIAL.
*          er_entity-gstin_bill_to = ls_taxnum-taxnum.
*       ELSE.
*          er_entity-gstin_bill_to = ls_taxnum-taxnumxl.
*       ENDIF.
*     ENDIF.

      IF ls_customer_re-customer-stcd3 IS NOT INITIAL.
        er_entity-gstin_bill_to = ls_customer_re-customer-stcd3.
      ENDIF.

*-- To Fetch the Ship To Party GSTIN
*    CLEAR: ls_vbpa.
**           lt_taxnum.
*    READ TABLE lt_vbpa INTO ls_vbpa WITH KEY parvw = lc_parvw_we.
*    IF sy-subrc = 0.
*      CALL FUNCTION 'BUPA_TAX_SELECT_WITH_PARTNER'
*          EXPORTING
*            iv_partner     = ls_vbpa-kunnr
*            iv_addrnumber  = ls_vbpa-adrnr
*          TABLES
*            et_tax_numbers = lt_taxnum.

*       CLEAR: ls_customer.
**       DATA(lo_bp1) = cl_glo_log_utilities=>get_instance( ).
*
*       CALL METHOD lo_bp1->get_customer_tax_details
*          EXPORTING
*            iv_customer     = ls_vbpa-kunnr
*            iv_address      = ls_vbpa-adrnr
*            iv_adr_ind      = ls_vbpa-adrda
*            iv_bp_ref_adrnr = ls_vbpa-bp_ref_adrnr
*            iv_stceg        = ls_vbpa-stceg
*          receiving
*            rs_customer     = ls_customer.

        IF ls_customer_we-customer-stcd3 IS NOT INITIAL.
          er_entity-gstin_ship_to = ls_customer_we-customer-stcd3.
        ENDIF.

      TEST-SEAM ts_tnum.
      END-TEST-SEAM.

*      IF lt_taxnum IS NOT INITIAL.
*        CLEAR: ls_taxnum.
*        READ TABLE lt_taxnum INTO ls_taxnum WITH KEY taxtype = lc_taxtype_in.
*        IF sy-subrc = 0.
*           IF ls_taxnum-taxnum IS NOT INITIAL.
*              er_entity-gstin_ship_to = ls_taxnum-taxnum.
*           ELSE.
*              er_entity-gstin_ship_to = ls_taxnum-taxnumxl.
*           ENDIF.
*        ENDIF.
*      ENDIF.
*    ENDIF.

ENDIF.
*-- Changes for Egypt Invoice forms
*-- Fetch Company & Customer identification number
 IF ms_billing_document-landtx = lc_country_eg.

    SELECT SINGLE paval FROM T001Z INTO er_entity-vat_reg_no_company WHERE BUKRS = ms_billing_document-bukrs
                                            AND PARTY = '0EGTRN'.

 ENDIF.


  ENDMETHOD.


  METHOD vatsummary_get_entityset.

    CONSTANTS : lc_country_pl TYPE string VALUE 'PL'.

    FIELD-SYMBOLS: <fs_tab_entityset> LIKE LINE OF et_entityset.

    DATA: lv_gjahr TYPE bkpf-gjahr,
          lv_belnr TYPE bkpf-belnr,
          lt_bset  TYPE  STANDARD TABLE OF BSET,
          wa_bset  TYPE bset.

    TRY.
        CALL METHOD super->vatsummary_get_entityset
          EXPORTING
            iv_entity_name           = iv_entity_name
            iv_entity_set_name       = iv_entity_set_name
            iv_source_name           = iv_source_name
            it_filter_select_options = it_filter_select_options
            is_paging                = is_paging
            it_key_tab               = it_key_tab
            it_navigation_path       = it_navigation_path
            it_order                 = it_order
            iv_filter_string         = iv_filter_string
            iv_search_string         = iv_search_string
            io_tech_request_context  = io_tech_request_context
          IMPORTING
            et_entityset             = et_entityset
            es_response_context      = es_response_context.
      CATCH /iwbep/cx_mgw_busi_exception .
      CATCH /iwbep/cx_mgw_tech_exception .
    ENDTRY.

    TEST-SEAM fill_et4.
    END-TEST-SEAM.


*** To fetch VAT Amount from BSET table for below scenario
*** 1. possiblity of one accounting document having vat amount
*** 2. BSET  table recordsd will be based on the tax code not line item.

    If ms_billing_document-landtx = lc_country_pl and et_entityset is not INITIAL.
      SELECT SINGLE gjahr FROM vbrk
                    INTO lv_gjahr
                    WHERE vbeln = ms_billing_document-vbeln.

      SELECT SINGLE belnr FROM bkpf
               INTO lv_belnr
               WHERE bukrs = ms_billing_document-bukrs
               AND   gjahr = lv_gjahr
               AND   xblnr = ms_billing_document-vbeln
               AND   bstat = ' '
               AND   GLVOR = 'SD00'.

      SELECT mwskz hwste FROM BSET
               INTO CORRESPONDING FIELDS OF TABLE lt_bset WHERE bukrs = ms_billing_document-bukrs
                                    AND gjahr = lv_gjahr
                                    AND belnr = lv_belnr.
      TEST-SEAM ts_bl.
      END-TEST-SEAM.
      IF lt_bset IS NOT INITIAL.
        LOOP AT et_entityset ASSIGNING <fs_tab_entityset>.
          READ TABLE lt_bset INTO wa_bset WITH KEY mwskz = <fs_tab_entityset>-tax_code.
          If sy-subrc = 0.
            <fs_tab_entityset>-cndn_amount_in_cocode_crcy = wa_bset-hwste.
          ENDIF.
        ENDLOOP.
      ENDIF.
    ENDIF.

*** Poland Correction Invoice Form
    IF ms_billing_document-landtx = lc_country_pl
             AND ms_billing_document-vbtyp EQ 'O'.      " Correction Invoice

      LOOP AT et_entityset ASSIGNING <fs_tab_entityset>.

        IF <fs_tab_entityset>-condition_base_value <> 0.
          <fs_tab_entityset>-condition_base_value = <fs_tab_entityset>-condition_base_value * -1. " Reverse the sign
        ENDIF.

        IF <fs_tab_entityset>-cndn_amount_in_cocode_crcy <> 0.
          <fs_tab_entityset>-cndn_amount_in_cocode_crcy = <fs_tab_entityset>-cndn_amount_in_cocode_crcy * -1. " Reverse the sign
        ENDIF.

      ENDLOOP.

    ENDIF.

  ENDMETHOD.
ENDCLASS.
*******************************************************************************************************************************************

CLASS zcl_zexporttaxinv_dpc_ext DEFINITION
  PUBLIC
  INHERITING FROM zcl_zexporttaxinv_dpc
  CREATE PUBLIC .

  PUBLIC SECTION.

    TYPES:
      BEGIN OF ty_billingdoc,
        vbeln                      TYPE  vbrk-vbeln,
        bukrs                      TYPE  vbrk-bukrs,
        zterms                     TYPE  vbrk-zterm,
        xblnr                      TYPE  vbrk-xblnr,
        fkdat                      TYPE  vbrk-fkdat,
        inco1                      TYPE  vbrk-inco1,
        inco2                      TYPE  vbrk-inco2,
        vkorg                      TYPE  vbrk-vkorg,
        vtweg                      TYPE  vbrk-vtweg,
        kunag                      TYPE  vbrk-kunag,
        bupla                      TYPE  vbrk-bupla,
        fkart                      TYPE  vbrk-fkart,
        posnr                      TYPE  i_billingdocextditembasic-billingdocumentitem,
        knumv_ana                  TYPE  i_billingdocextditembasic-pricingdocument,
        matnr                      TYPE  i_billingdocextditembasic-material,
        werks                      TYPE  i_billingdocextditembasic-plant,
        aubel                      TYPE  i_billingdocextditembasic-salesdocument,
        kunwe                      TYPE  i_billingdocextditembasic-shiptoparty,
        arktx                      TYPE  i_billingdocextditembasic-billingdocumentitemtext,
        vrkme                      TYPE  i_billingdocextditembasic-billingquantityunit,
        fkimg                      TYPE  i_billingdocextditembasic-billingquantity,
        netwr                      TYPE  i_billingdocextditembasic-netamount,
        spart                      TYPE  vbrk-spart,
        zz1_shipfrom_bdh           TYPE  vbrk-zz1_shipfrom_bdh,
        zz1_transportvendorco_bdh  TYPE  vbrk-zz1_transportvendorco_bdh,
        zz1_modeofdel_bdh          TYPE  vbrk-zz1_modeofdel_bdh,
        zz1_vehiclenumber_bdh      TYPE  vbrk-zz1_vehiclenumber_bdh,
        zz1_vehicletype_bdh        TYPE  vbrk-zz1_vehicletype_bdh,
        zz1_distance_bdh           TYPE  vbrk-zz1_distance_bdh,
        zz1_lrnumber_bdh           TYPE  vbrk-zz1_lrnumber_bdh,
        zz1_lrdate_bdh             TYPE  vbrk-zz1_lrdate_bdh,
        kurrf                      TYPE  vbrk-kurrf,
        landtx                     TYPE  vbrk-landtx,
        land1                      TYPE  vbrk-land1,
        licencenumber              TYPE  vbrk-zz1_rodteplicenseno_bdh, "Added by Vaishnavi Vairagare
        zz1_vendorgstinnumber_bdh  TYPE  vbrk-zz1_vendorgstinnumber_bdh,
        zz1_transportvendorgst_bdh TYPE vbrk-zz1_transportvendorgst_bdh,
      END OF ty_billingdoc .
    TYPES:
      tt_billingdoc TYPE TABLE OF ty_billingdoc WITH EMPTY KEY .

    CLASS-DATA billingdata TYPE tt_billingdoc .
    CLASS-DATA suppliercode TYPE zsdsupcodelut-suppliercode .
    CLASS-DATA amtinwords TYPE pc207-betrg .
    CLASS-DATA invoiceamt TYPE pc207-betrg .

    METHODS /iwbep/if_mgw_appl_srv_runtime~get_entity
        REDEFINITION .
    METHODS /iwbep/if_mgw_appl_srv_runtime~get_entityset
        REDEFINITION .
PROTECTED SECTION.

  METHODS footer_get_entityset
    IMPORTING
      !iv_entity_name           TYPE string
      !iv_entity_set_name       TYPE string
      !iv_source_name           TYPE string
      !it_filter_select_options TYPE /iwbep/t_mgw_select_option
      !is_paging                TYPE /iwbep/s_mgw_paging
      !it_key_tab               TYPE /iwbep/t_mgw_name_value_pair
      !it_navigation_path       TYPE /iwbep/t_mgw_navigation_path
      !it_order                 TYPE /iwbep/t_mgw_sorting_order
      !iv_filter_string         TYPE string
      !iv_search_string         TYPE string
      !io_tech_request_context  TYPE REF TO /iwbep/if_mgw_req_entityset OPTIONAL
    EXPORTING
      !et_entityset             TYPE zcl_zexporttaxinv_mpc=>tt_footer
      !es_response_context      TYPE /iwbep/if_mgw_appl_srv_runtime=>ty_s_mgw_response_context
    RAISING
      /iwbep/cx_mgw_busi_exception
      /iwbep/cx_mgw_tech_exception .
  METHODS header_get_entity
    IMPORTING
      !iv_entity_name          TYPE string
      !iv_entity_set_name      TYPE string
      !iv_source_name          TYPE string
      !it_key_tab              TYPE /iwbep/t_mgw_name_value_pair
      !io_request_object       TYPE REF TO /iwbep/if_mgw_req_entity OPTIONAL
      !io_tech_request_context TYPE REF TO /iwbep/if_mgw_req_entity OPTIONAL
      !it_navigation_path      TYPE /iwbep/t_mgw_navigation_path
    EXPORTING
      !er_entity               TYPE zcl_zexporttaxinv_mpc=>ts_header
      !es_response_context     TYPE /iwbep/if_mgw_appl_srv_runtime=>ty_s_mgw_response_entity_cntxt
    RAISING
      /iwbep/cx_mgw_busi_exception
      /iwbep/cx_mgw_tech_exception .
  METHODS item_get_entity
    IMPORTING
      !iv_entity_name           TYPE string
      !iv_entity_set_name       TYPE string
      !iv_source_name           TYPE string
      !it_filter_select_options TYPE /iwbep/t_mgw_select_option
      !is_paging                TYPE /iwbep/s_mgw_paging
      !it_key_tab               TYPE /iwbep/t_mgw_name_value_pair
      !it_navigation_path       TYPE /iwbep/t_mgw_navigation_path
      !it_order                 TYPE /iwbep/t_mgw_sorting_order
      !iv_filter_string         TYPE string
      !iv_search_string         TYPE string
      !io_tech_request_context  TYPE REF TO /iwbep/if_mgw_req_entityset OPTIONAL
    EXPORTING
*      !et_entityset             TYPE zcl_zexporttaxinv_mpc=>tt_itemdat001
      !et_entityset             TYPE zcl_zexporttaxinv_mpc=>tt_itemdata
      !es_response_context      TYPE /iwbep/if_mgw_appl_srv_runtime=>ty_s_mgw_response_context
    RAISING
      /iwbep/cx_mgw_busi_exception
      /iwbep/cx_mgw_tech_exception .
private section.
ENDCLASS.



CLASS ZCL_ZEXPORTTAXINV_DPC_EXT IMPLEMENTATION.


  METHOD /iwbep/if_mgw_appl_srv_runtime~get_entity.
**TRY.
*CALL METHOD SUPER->/IWBEP/IF_MGW_APPL_SRV_RUNTIME~GET_ENTITY
**  EXPORTING
**    iv_entity_name          =
**    iv_entity_set_name      =
**    iv_source_name          =
**    it_key_tab              =
**    it_navigation_path      =
**    io_tech_request_context =
**  IMPORTING
**    er_entity               =
**    es_response_context     =
*    .
**  CATCH /iwbep/cx_mgw_busi_exception.
**  CATCH /iwbep/cx_mgw_tech_exception.
**ENDTRY.

    DATA(lv_entityset) = io_tech_request_context->get_entity_set_name( ).
    CASE lv_entityset.
      WHEN 'HeaderSet'.
        TRY.
            CALL METHOD header_get_entity
              EXPORTING
                iv_entity_name      = iv_entity_name
                iv_entity_set_name  = iv_entity_set_name
                iv_source_name      = iv_source_name
                it_key_tab          = it_key_tab                            " table for name value pairs
*               io_request_object   =                  " table of navigation paths
*               io_tech_request_context =
                it_navigation_path  = it_navigation_path                " table of navigation paths
              IMPORTING
                er_entity           = DATA(header_data)                " Returning data
                es_response_context = es_response_context.
          CATCH /iwbep/cx_mgw_busi_exception. " business exception in mgw
          CATCH /iwbep/cx_mgw_tech_exception. " mgw technical exception
        ENDTRY.

        copy_data_to_ref(
         EXPORTING
           is_data = header_data
         CHANGING
           cr_data = er_entity ).

      WHEN OTHERS.

        TRY.
            CALL METHOD super->/iwbep/if_mgw_appl_srv_runtime~get_entity
              EXPORTING
                iv_entity_name          = iv_entity_name
                iv_entity_set_name      = iv_entity_set_name
                iv_source_name          = iv_source_name
                it_key_tab              = it_key_tab
                it_navigation_path      = it_navigation_path
                io_tech_request_context = io_tech_request_context
              IMPORTING
                er_entity               = er_entity
                es_response_context     = es_response_context.
          CATCH /iwbep/cx_mgw_busi_exception.
          CATCH /iwbep/cx_mgw_tech_exception.
        ENDTRY.

    ENDCASE.


  ENDMETHOD.


  METHOD /iwbep/if_mgw_appl_srv_runtime~get_entityset.
**TRY.
*CALL METHOD SUPER->/IWBEP/IF_MGW_APPL_SRV_RUNTIME~GET_ENTITYSET
**  EXPORTING
**    iv_entity_name           =
**    iv_entity_set_name       =
**    iv_source_name           =
**    it_filter_select_options =
**    it_order                 =
**    is_paging                =
**    it_navigation_path       =
**    it_key_tab               =
**    iv_filter_string         =
**    iv_search_string         =
**    io_tech_request_context  =
**  IMPORTING
**    er_entityset             =
**    es_response_context      =
*    .
**  CATCH /iwbep/cx_mgw_busi_exception.
**  CATCH /iwbep/cx_mgw_tech_exception.
**ENDTRY.

    DATA(entityset) = io_tech_request_context->get_entity_set_name( ).
    IF entityset = 'ItemDataSet'.
      TRY.
          CALL METHOD item_get_entity
            EXPORTING
              iv_entity_name           = iv_entity_name
              iv_entity_set_name       = iv_entity_set_name
              iv_source_name           = iv_source_name
              it_filter_select_options = it_filter_select_options                 " Table of select options
              is_paging                = is_paging                                " Paging structure
              it_key_tab               = it_key_tab                               " Table for name value pairs
              it_navigation_path       = it_navigation_path                       " Table of navigation paths
              it_order                 = it_order                                 " The sorting order
              iv_filter_string         = iv_filter_string                         " Table for name value pairs
              iv_search_string         = iv_search_string
              io_tech_request_context  = io_tech_request_context
            IMPORTING
              et_entityset             = DATA(item_set)              " Returning data
              es_response_context      = es_response_context.

        CATCH /iwbep/cx_mgw_busi_exception.
        CATCH /iwbep/cx_mgw_tech_exception.
      ENDTRY.

      copy_data_to_ref(
           EXPORTING
             is_data = item_set
           CHANGING
             cr_data = er_entityset ).

    ELSEIF entityset = 'FooterSet'.
      TRY.
          CALL METHOD footer_get_entityset
            EXPORTING
              iv_entity_name           = iv_entity_name
              iv_entity_set_name       = iv_entity_set_name
              iv_source_name           = iv_source_name
              it_filter_select_options = it_filter_select_options                 " Table of select options
              is_paging                = is_paging                                " Paging structure
              it_key_tab               = it_key_tab                               " Table for name value pairs
              it_navigation_path       = it_navigation_path                       " Table of navigation paths
              it_order                 = it_order                                 " The sorting order
              iv_filter_string         = iv_filter_string                         " Table for name value pairs
              iv_search_string         = iv_search_string
*             io_tech_request_context  =
            IMPORTING
              et_entityset             = DATA(footerdatasets)              " Returning data
*             es_response_context      =
            .
        CATCH /iwbep/cx_mgw_busi_exception. " business exception in mgw
        CATCH /iwbep/cx_mgw_tech_exception. " mgw technical exception
      ENDTRY.
      copy_data_to_ref(
       EXPORTING
         is_data = footerdatasets

       CHANGING
         cr_data = er_entityset ).

    ELSE.
      TRY.
          CALL METHOD super->/iwbep/if_mgw_appl_srv_runtime~get_entityset
            EXPORTING
              iv_entity_name           = iv_entity_name
              iv_entity_set_name       = iv_entity_set_name
              iv_source_name           = iv_source_name
              it_filter_select_options = it_filter_select_options
              it_order                 = it_order
              is_paging                = is_paging
              it_navigation_path       = it_navigation_path
              it_key_tab               = it_key_tab
              iv_filter_string         = iv_filter_string
              iv_search_string         = iv_search_string
              io_tech_request_context  = io_tech_request_context
            IMPORTING
              er_entityset             = er_entityset
              es_response_context      = es_response_context.
        CATCH /iwbep/cx_mgw_busi_exception. " business exception in mgw
        CATCH /iwbep/cx_mgw_tech_exception. " mgw technical exception
      ENDTRY.
    ENDIF.

  ENDMETHOD.


  METHOD footer_get_entityset.
*----------------------------------------------------------------------*
* Class           ZCL_ZTAXINVOICE_DPC_EXT                              *
*----------------------------------------------------------------------*
* Title:          Dosmestic Tax Invoice                                *
* RICEF#:         RSB_SD_F_01                                          *
* Transaction:    VF01/VF02/VF03                                       *
*----------------------------------------------------------------------*
* Copyright:      NDBS, Inc.                                           *
* Client:         RSB Transmission                                     *
*----------------------------------------------------------------------*
* Developer:      NTT_ABAP5 ( Vaishnavi Vairagare )                    *
* Creation Date:  15/05/2025                                           *
* Description:    Domestic Tax Invoice                                 *
*----------------------------------------------------------------------*
* Modification History                                                 *
*----------------------------------------------------------------------*
* Modified by:    <Developer (full name and user name)>                *
* Date:           <Date>                                               *
* Transport:      <Transport Request #>                                *
* Description:                                                         *
*<Description of the change (or the source for the initial creation if *
* a template or SAP program was used as a starting point>              *
*----------------------------------------------------------------------*
    " Data Declaration For Billing Document Number.

    DATA(billingdocument) = VALUE #( it_key_tab[ name = 'BillingDocument' ]-value OPTIONAL ).

*    " Data Declarations
    DATA:
      footer            TYPE zcl_zexporttaxinv_mpc=>ts_footer,
      footerdata        TYPE zcl_zexporttaxinv_mpc_ext=>ty_footerdata,
      footertable       TYPE zcl_zexporttaxinv_mpc_ext=>tt_footertable,
      condition_type    TYPE RANGE OF prcd_elements-kschl,
      discounts         TYPE kbetr,
      igst              TYPE kbetr,
      sgstper           TYPE kbetr,
      cgstper           TYPE kbetr,
      tcsper            TYPE kbetr,
      dis               TYPE p DECIMALS 2,
      tatol_basic_value TYPE kbetr,
*      amtinwords        TYPE pc207-betrg,
*      invoiceamt        TYPE pc207-betrg,
      gstamt            TYPE char200,
      invamt            TYPE char200,
      totalbase         TYPE kbetr,
      qty_unit          TYPE netwr,
      exchangerate      TYPE vbrk-kurrf,
      netwr_value       TYPE netwr,
      amt_igstval       TYPE kbetr.

    "   Fetching ID's from TVARVC table
    SELECT
           name,
           low,
           high FROM tvarvc
                WHERE name = @text-001
                INTO TABLE @DATA(lt_tvarvc).            "#EC CI_NOORDER

    IF sy-subrc = 0.
      condition_type = VALUE #( FOR ls_tvarvc IN lt_tvarvc "#EC CI_STDSEQ
                              WHERE ( name = TEXT-001 ) "#EC CI_STDSEQ "ZMM_RFQ_TEXTIDS
                                    ( sign = |{ /isdfps/cl_const_abc_123=>gc_i }|
                                      option = |{ /isdfps/cl_const_abc_123=>gc_e && /isdfps/cl_const_abc_123=>gc_q }|
                                      low  = ls_tvarvc-low ) ).
    ENDIF.
*
    IF billingdocument IS NOT INITIAL.
      " Combination of Billing Document Header and Item Table and storing all the values in one internal table
      SELECT _vbrk~vbeln                     AS vbeln,
             _vbrk~bukrs                     AS bukrs,
             _vbrk~zterm                     AS zterms,
             _vbrk~xblnr                     AS xblnr,
             _vbrk~fkdat                     AS fkdat,
             _vbrk~inco1                     AS inco1,
             _vbrk~inco2                     AS inco2,
             _vbrk~vkorg                     AS vkorg,
             _vbrk~vtweg                     AS vtweg,
             _vbrk~kunag                     AS kunag,
             _vbrk~bupla                     AS bupla,
             _vbrk~fkart                     AS fkart,
             _vbrp~billingdocumentitem       AS posnr,
             _vbrp~pricingdocument           AS knumv_ana,
             _vbrp~material                  AS matnr,
             _vbrp~plant                     AS werks,
             _vbrp~salesdocument             AS aubel,
             _vbrp~shiptoparty               AS kunwe,
             _vbrp~billingdocumentitemtext   AS arktx,
             _vbrp~billingquantityunit       AS vrkme,
             _vbrp~billingquantity           AS fkimg,
             _vbrp~netamount                 AS netwr,
             _vbrk~spart                     AS spart,
             _vbrk~zz1_shipfrom_bdh          AS zz1_shipfrom_bdh,
            _vbrk~zz1_transportvendorco_bdh  AS zz1_transportvendorco_bdh,
            _vbrk~zz1_modeofdel_bdh          AS zz1_modeofdel_bdh,
            _vbrk~zz1_vehiclenumber_bdh      AS zz1_vehiclenumber_bdh,
            _vbrk~zz1_vehicletype_bdh        AS zz1_vehicletype_bdh,
            _vbrk~zz1_distance_bdh           AS zz1_distance_bdh,
            _vbrk~zz1_lrnumber_bdh           AS zz1_lrnumber_bdh,
            _vbrk~zz1_lrdate_bdh             AS zz1_lrdate_bdh,
            _vbrk~kurrf,
            _vbrk~landtx,
            _vbrk~land1,
            _vbrk~zz1_rodteplicenseno_bdh      AS licencenumber,
             _vbrk~zz1_vendorgstinnumber_bdh  AS transportvendorgstinno, "Added
            _vbrk~zz1_transportvendorgst_bdh AS transportvendorgstinname "added
             FROM vbrk     AS _vbrk
             INNER JOIN i_billingdocextditembasic AS _vbrp ON _vbrk~vbeln = _vbrp~billingdocument
             WHERE _vbrk~vbeln = @billingdocument
             INTO TABLE @billingdata.
*
    ENDIF.
*
    IF billingdata IS NOT INITIAL.

      SELECT billingdocument AS vbeln,
             totalnetamount  AS netwr FROM i_billingdocumentbasic AS _billdoc
                                      INTO TABLE @DATA(taxablevalue)
                                      WHERE _billdoc~billingdocument = @billingdocument.
      IF sy-subrc = 0.
      ENDIF.

      SELECT vbrkvbrp~vbeln    AS vbeln,
            vbrkvbrp~aubel     AS aubel,
            vbrkvbrp~knumv_ana AS knumv_ana,
            vbrkvbrp~posnr     AS posnr,
            vbrkvbrp~matnr     AS material_code,
            vbrkvbrp~arktx     AS material_description,
            vbrkvbrp~vrkme     AS uom,
            vbrkvbrp~fkimg     AS quantity,
            vbrkvbrp~netwr     AS taxablevalue,
            vbrkvbrp~netwr,
            vbrkvbrp~vkorg     AS vkorg,
            vbrkvbrp~fkdat,
            vbrkvbrp~kunag,
            vbap~kdmat         AS customer_material_code,
            vbrkvbrp~vtweg     AS vtweg,
            vbrkvbrp~kurrf
            FROM @billingdata  AS vbrkvbrp
            LEFT OUTER JOIN vbap ON vbap~vbeln = vbrkvbrp~aubel
            AND vbap~posnr = vbrkvbrp~posnr
            WHERE vbrkvbrp~vbeln = @billingdocument
       INTO TABLE @DATA(itemdetails).
      IF sy-subrc = 0.
      ENDIF.

      SELECT
        vbrkvbrp~vbeln AS vbeln,
        vbrkvbrp~posnr,
        vbrkvbrp~knumv_ana,
*        vbrkvbrp~netwr,
        prcd_elements~kposn,
        prcd_elements~knumv,
        prcd_elements~kbetr,
        prcd_elements~kschl,
        prcd_elements~kwert
            FROM @billingdata AS vbrkvbrp
            LEFT OUTER JOIN prcd_elements ON prcd_elements~kposn = vbrkvbrp~posnr
                                          AND prcd_elements~knumv  = vbrkvbrp~knumv_ana
*                                          AND prcd_elements~kschl IN ( 'ZPR0' )
                                          AND prcd_elements~kschl IN ( 'ZPR0' , 'ZBLK' , 'ZCDS' , 'ZBD1' , 'ZADC' , 'ZFLD' ,
                                                                       'ZFRE' , 'ZPAC' , 'ZTAC' , 'JOIG' , 'JOCG' , 'JOSG' ,
                                                                       'JTC2'  )
            WHERE vbrkvbrp~vbeln = @billingdocument
            INTO TABLE @DATA(pricing).

      IF sy-subrc = 0.
      ENDIF.

      SELECT
        vbrkvbrp~vbeln,
        vbrkvbrp~matnr,
        vbrkvbrp~landtx,
*        vbrkvbrp~netwr,
        vbrkvbrp~land1,
        marc~steuc
                  FROM @billingdata AS vbrkvbrp
                  LEFT OUTER JOIN marc ON marc~matnr = vbrkvbrp~matnr
                    WHERE vbrkvbrp~vbeln = @billingdocument
        INTO TABLE @DATA(marcval).

      IF sy-subrc = 0.
      ENDIF.

      SELECT
        marcval~vbeln,
        a4ap~knumh,
        konp~kbetr
                  FROM @marcval AS marcval
                  LEFT OUTER JOIN a4ap ON a4ap~aland  = marcval~landtx
                                       AND a4ap~land1 = marcval~land1
                                       AND a4ap~steuc = marcval~steuc
                  LEFT OUTER JOIN konp ON konp~knumh  = a4ap~knumh
                  WHERE marcval~vbeln = @billingdocument
                  INTO TABLE @DATA(gstvalue).

      IF itemdetails IS NOT INITIAL.
        LOOP AT itemdetails ASSIGNING FIELD-SYMBOL(<fs_item>).
          exchangerate                        = <fs_item>-kurrf.
          footerdata-billingdocument          = <fs_item>-vbeln.
          footerdata-posnr                    = <fs_item>-posnr.
          netwr_value                         = VALUE #( taxablevalue[ vbeln = billingdocument ]-netwr OPTIONAL ).
          footerdata-unitprice                =  VALUE #( pricing[ kposn = <fs_item>-posnr kschl = 'ZPR0' ]-kbetr OPTIONAL ) * exchangerate.
          footerdata-quntity                  = <fs_item>-quantity.
          qty_unit                            = footerdata-quntity * footerdata-unitprice.
          footerdata-dist                     = REDUCE vfprc_element_amount( INIT lv_dist TYPE vfprc_element_amount "#EC CI_STDSEQ
                                                                             FOR ls_pricing IN pricing
                                                                             WHERE ( knumv = <fs_item>-knumv_ana
                                                                             AND kposn = <fs_item>-posnr
                                                                             AND kschl IN condition_type )
                                                 NEXT lv_dist = lv_dist + ls_pricing-kbetr ) * ( -1 ).
          IF footerdata-dist  > '0.00'.
            footerdata-discount                    = |{ footerdata-dist }{ '%' }|.
          ENDIF.
          dis                                  = ( discounts / 100 ) * footerdata-unitprice.
          DATA(emptyvalue)                  = COND #( WHEN discounts = '0.0' OR footerdata-discount = '0.0%'
                                                         THEN ''
                                                         ELSE 'X' ).
          footerdata-footerdisval                = qty_unit * ( footerdata-dist / 100 ).
          igst                                 = REDUCE vfprc_element_amount( INIT lv_gst TYPE vfprc_element_amount "#EC CI_STDSEQ
                                                                              FOR ls_gst IN gstvalue
                                                                              WHERE (  vbeln = billingdocument )
                                                 NEXT lv_gst =  ls_gst-kbetr ) / 10.
          IF igst IS NOT INITIAL.
            footerdata-igst = |{ igst }{ '%' }|.
          ENDIF.
          footerdata-igstval  = ( netwr_value * exchangerate ) * igst / 100.
*          footerdata-igstval  = igst / 100.
          amt_igstval         = footerdata-igstval.
          footerdata-freight              = REDUCE vfprc_element_value( INIT lv_freight TYPE vfprc_element_value "#EC CI_STDSEQ
                                                                    FOR ls_pricing IN pricing
                                                                    WHERE ( vbeln = billingdocument
                                                                    AND knumv_ana = <fs_item>-knumv_ana
                                                                    AND kposn = <fs_item>-posnr
                                                                    AND kschl = 'ZFRE' )
                                                                    NEXT lv_freight = lv_freight + ls_pricing-kwert ).

          footerdata-packing            = REDUCE vfprc_element_amount( INIT lv_packag TYPE vfprc_element_value "#EC CI_STDSEQ
                                                                       FOR ls_pricing IN pricing
                                                                       WHERE (  vbeln = billingdocument
                                                                       AND knumv_ana = <fs_item>-knumv_ana
                                                                       AND kposn = <fs_item>-posnr
                                                                       AND kschl = 'ZPAC' )
                                                                       NEXT lv_packag = lv_packag + ls_pricing-kwert ).

          footerdata-toolamortization    = REDUCE vfprc_element_value( INIT lv_toot TYPE vfprc_element_value "#EC CI_STDSEQ
                                                                       FOR ls_pricing IN pricing
                                                                       WHERE (  vbeln = billingdocument
                                                                       AND knumv_ana = <fs_item>-knumv_ana
                                                                       AND kposn = <fs_item>-posnr
                                                                       AND kschl = 'ZTAC' )
                                                                       NEXT lv_toot = lv_toot + ls_pricing-kwert ).

          footerdata-totalbasic             = REDUCE vfprc_element_value( INIT lv_totalbasic TYPE vfprc_element_value "#EC CI_STDSEQ
                                                                             FOR ls_pricing IN pricing
                                                                             WHERE ( vbeln = billingdocument
                                                                             AND knumv_ana = <fs_item>-knumv_ana
                                                                             AND kposn = <fs_item>-posnr
                                                                             AND kschl = 'ZPR0' )
                                                 NEXT lv_totalbasic = ls_pricing-kwert ) * exchangerate.

          APPEND footerdata TO footertable.
          CLEAR footerdata.
        ENDLOOP.
      ENDIF.

      " Start of changes on 08.12.2025

      footerdata-freight  =  REDUCE vfprc_element_value( INIT lv_freight TYPE vfprc_element_value "#EC CI_STDSEQ
                                                         FOR footerwork IN footertable
                             NEXT lv_freight = lv_freight + footerwork-freight ).

      footerdata-packing  =  REDUCE vfprc_element_value( INIT lv_packing TYPE vfprc_element_value "#EC CI_STDSEQ
                                                         FOR footerwork IN footertable
                             NEXT lv_packing = lv_packing + footerwork-packing ).

      footerdata-toolamortization  =  REDUCE vfprc_element_value( INIT lv_toolamortization TYPE vfprc_element_value "#EC CI_STDSEQ
                                                                  FOR footerwork IN footertable
                                      NEXT lv_toolamortization = lv_toolamortization + footerwork-toolamortization ).

      " End of changes on 08.12.2025

      footerdata-disval  =  REDUCE netwr( INIT lv_disvalue TYPE netwr "#EC CI_STDSEQ
                                                   FOR footerwork IN footertable
                                                   NEXT lv_disvalue = lv_disvalue + footerwork-footerdisval ).

      IF taxablevalue IS NOT INITIAL.
        footerdata-taxablevalue = VALUE #( taxablevalue[ vbeln = billingdocument ]-netwr OPTIONAL ) * exchangerate.
        DATA(taxable) = footerdata-taxablevalue ."* exchangerate.
      ENDIF.

      " Total Basic Value
      footerdata-totalbasic = REDUCE fkimg( INIT lv_bas TYPE fkimg "#EC CI_STDSEQ
                                            FOR footerwork IN footertable
                                            NEXT lv_bas = lv_bas + footerwork-totalbasic ) .

      " Displaying GST amount
      amtinwords = amt_igstval.

      DATA :  inv_val TYPE p LENGTH 16 DECIMALS 3.
      "Displaying this amount in words for Total Invoice value ( Taxable value + GST values )
      inv_val = footerdata-taxablevalue + amt_igstval.
      invoiceamt =  inv_val .

      MODIFY footertable FROM VALUE #(  disval       = footerdata-disval
                                        totalbasic   = footerdata-totalbasic
                                        " Start of changes 08.12.2025
                                        freight          = footerdata-freight
                                        packing          = footerdata-packing
                                        toolamortization = footerdata-toolamortization
                                        " End of changes 08.12.2025
                                        taxablevalue = footerdata-taxablevalue  )
      TRANSPORTING
                   taxablevalue disval  totalbasic freight packing toolamortization
      WHERE billingdocument IS NOT INITIAL.

      LOOP AT footertable ASSIGNING FIELD-SYMBOL(<fs_footer>).
        IF <fs_footer>-totalbasic IS NOT INITIAL.
          footer-name = COND #( WHEN <fs_footer>-totalbasic IS NOT INITIAL
                                          THEN 'Total Basic Value' ).
          footer-value = COND #( WHEN <fs_footer>-totalbasic IS NOT INITIAL
                                          THEN <fs_footer>-totalbasic  ).
          APPEND footer TO et_entityset.
          CLEAR footer.
        ENDIF.

        IF <fs_footer>-footerdisval IS NOT INITIAL .
          footer-name = COND #( WHEN <fs_footer>-footerdisval IS NOT INITIAL
                                          THEN 'Discount' ).
          footer-value = COND #( WHEN <fs_footer>-footerdisval IS NOT INITIAL
                                          THEN <fs_footer>-disval  ).
          APPEND footer TO et_entityset.
          CLEAR footer.
        ENDIF.

        IF <fs_footer>-taxablevalue IS NOT INITIAL.
          footer-name = COND #( WHEN <fs_footer>-taxablevalue IS NOT INITIAL
                                          THEN 'Taxable Value' ).
          footer-value = COND #( WHEN <fs_footer>-taxablevalue IS NOT INITIAL
                                          THEN <fs_footer>-taxablevalue  ).
          APPEND footer TO et_entityset.
          CLEAR footer.
        ENDIF.

        IF <fs_footer>-freight IS NOT INITIAL.
          footer-name = COND #( WHEN <fs_footer>-freight IS NOT INITIAL
                                          THEN 'Freight Charges' ).
          footer-value = COND #( WHEN <fs_footer>-freight IS NOT INITIAL
                                          THEN <fs_footer>-freight  ).
          APPEND footer TO et_entityset.
        ENDIF.

        IF <fs_footer>-packing IS NOT INITIAL.
          footer-name = COND #( WHEN <fs_footer>-packing IS NOT INITIAL
                                          THEN 'Packing Charges' ).
          footer-value = COND #( WHEN <fs_footer>-packing IS NOT INITIAL
                                          THEN <fs_footer>-packing  ).
          APPEND footer TO et_entityset.
          CLEAR footer.
        ENDIF.

        IF <fs_footer>-toolamortization IS NOT INITIAL.
          footer-name = COND #( WHEN <fs_footer>-toolamortization IS NOT INITIAL
                                          THEN 'Tool Amortization' ).
          footer-value = COND #( WHEN <fs_footer>-toolamortization IS NOT INITIAL
                                          THEN <fs_footer>-toolamortization  ).
          APPEND footer TO et_entityset.
          CLEAR footer.
        ENDIF.

        IF <fs_footer>-igst IS NOT INITIAL AND <fs_footer>-igstval IS NOT INITIAL.
          footer-name        =  COND #( WHEN <fs_footer>-igst IS NOT INITIAL
                                        THEN 'IGST' ).
          footer-namesign       =  COND #( WHEN <fs_footer>-igst IS NOT INITIAL
                                        THEN '@'  ).
          footer-namesignval    =  COND #( WHEN <fs_footer>-igst IS NOT INITIAL
                                        THEN <fs_footer>-igst ).
          footer-value =  COND #( WHEN <fs_footer>-igstval IS NOT INITIAL
                                        THEN <fs_footer>-igstval  ).
          APPEND footer TO et_entityset.
          CLEAR footer.
        ENDIF.

        EXIT.
      ENDLOOP.

    ENDIF.
  ENDMETHOD.


  METHOD header_get_entity.
*----------------------------------------------------------------------*
* Class           ZCL_ZTAXINVOICE_DPC_EXT                              *
*----------------------------------------------------------------------*
* Title:          Dosmestic Tax Invoice                                *
* RICEF#:         RSB_SD_F_01                                          *
* Transaction:    VF01/VF02/VF03                                       *
*----------------------------------------------------------------------*
* Copyright:      NDBS, Inc.                                           *
* Client:         RSB Transmission                                     *
*----------------------------------------------------------------------*
* Developer:      NTT_ABAP5 ( Vaishnavi Vairagare )                    *
* Creation Date:  15/05/2025                                           *
* Description:    Domestic Tax Invoice                                 *
*----------------------------------------------------------------------*
* Modification History                                                 *
*----------------------------------------------------------------------*
* Modified by:    <Developer (full name and user name)>                *
* Date:           <Date>                                               *
* Transport:      <Transport Request #>                                *
* Description:                                                         *
*<Description of the change (or the source for the initial creation if *
* a template or SAP program was used as a starting point>              *
*----------------------------------------------------------------------*
    " Data Declaration For Billing Document Number.
    DATA(billingdocument) = VALUE #( it_key_tab[ name = 'BillingDocument' ]-value OPTIONAL ).
*
    DATA : billingdocno TYPE tdobname,
           vehicletype  TYPE string,
           vehicleno    TYPE string,
           distance     TYPE string,
           lrdocketno   TYPE string,
           lrdocketdate TYPE string,
*           remarks      TYPE string,
           gst          TYPE RANGE OF dfkkbptaxnum-partner.

    IF billingdocument IS NOT INITIAL.

      IF billingdata IS NOT INITIAL.
        " Fetching B2b & B2C , Customer PO Number and Customer Po Date
        SELECT
              vbrkvbrp~vbeln,
              vbrkvbrp~kunag,
              vbrkvbrp~vbeln                 AS reference,
              vbrkvbrp~zterms                AS paymentterms,
              tvzbt~vtext                    AS paymenttermsdescription,
              vbrkvbrp~xblnr                 AS invoice,
              vbrkvbrp~fkdat                 AS invoicedate,
              vbrkvbrp~inco1                 AS inco1,
              vbrkvbrp~inco2                 AS inco2,
              knvv~kvgr2                     AS taxnum,
              vbkd~purchaseorderbycustomer   AS customerpo,
              vbkd~customerpurchaseorderdate AS customerdate,
              zsd_e_invoice~zirn_no          AS irn,
              zsd_e_invoice~zewaybill_no     AS ewaybillno,
              zsd_e_invoice~zewb_gen_date    AS ewaybilldate,
              vbrkvbrp~fkart                 AS fkart,
              vbrkvbrp~licencenumber
              FROM @billingdata AS vbrkvbrp
              LEFT OUTER JOIN knvv ON  vbrkvbrp~kunag = knvv~kunnr
                                   AND vbrkvbrp~spart = knvv~spart
                                   AND vbrkvbrp~vkorg = knvv~vkorg
                                   AND vbrkvbrp~vtweg = knvv~vtweg
              LEFT OUTER JOIN i_salesdocumentitem        AS vbkd         ON  vbrkvbrp~aubel = vbkd~salesdocument
              LEFT OUTER JOIN tvzbt                      AS tvzbt        ON  tvzbt~zterm    = vbrkvbrp~zterms
                                                                         AND tvzbt~spras    = @sy-langu
              LEFT OUTER JOIN zsd_e_invoice   ON zsd_e_invoice~vbeln = vbrkvbrp~vbeln
              WHERE vbrkvbrp~vbeln = @billingdocument INTO TABLE @DATA(customerdetails).

        IF customerdetails IS NOT INITIAL.
          ASSIGN customerdetails[ vbeln = billingdocument ] TO FIELD-SYMBOL(<fs_customer>). "#EC CI_STDSEQ
          IF <fs_customer> IS ASSIGNED.
            er_entity-taxno          = <fs_customer>-taxnum.

            IF er_entity-taxno  = 'B2B'.
              er_entity-einv = 'E-Invoice QRC'.
            ELSEIF er_entity-taxno = 'B2C'.
              er_entity-einv = 'Dynamic QRC'.
            ENDIF.

            er_entity-licencenumber  = <fs_customer>-licencenumber.
            er_entity-reference      = <fs_customer>-reference.
            er_entity-invoice        = <fs_customer>-invoice.
            er_entity-invoicedate    = <fs_customer>-invoicedate.
            er_entity-customerpono   = <fs_customer>-customerpo.
            er_entity-customerpodate = <fs_customer>-customerdate.
            er_entity-paymentterms   = |{ <fs_customer>-paymentterms } { <fs_customer>-paymenttermsdescription }|.
            er_entity-incoterms      = |{ <fs_customer>-inco1 } { <fs_customer>-inco2 }|.
            er_entity-irn            = <fs_customer>-irn.
            er_entity-ewaybillno     = <fs_customer>-ewaybillno.
            er_entity-ewaybilldate   = <fs_customer>-ewaybilldate.
            er_entity-customerjob   = COND #( WHEN VALUE #( customerdetails[ vbeln = billingdocument fkart = 'ZSW' ]-fkart OPTIONAL ) = 'ZSW'
                                              THEN '1'
                                              ELSE '0' ).
          ENDIF.
          UNASSIGN <fs_customer>.
        ENDIF.

        " Fetching Data for Billing From Address Details
        SELECT
              vbrkvbrp~vbeln                  AS vbeln,
              vbrkvbrp~werks                  AS billfrom_plant,
              adrc~addresseename1             AS billfrom_name1,
              adrc~addresseename2             AS billfrom_name2,
              adrc~streetname                 AS billfrom_street,
              adrc~cityname                   AS billfrom_city1,
              adrc~postalcode                 AS billfrom_postcode,
              t005u~regionname                AS billfrom_regiondescription,
              j_1bbranch~gstin                AS billfrom_gstin,
              t001z~companycodeparametervalue AS billfrom_pan,
              t001z~companycodeparametervalue AS billfrom_iec,
              t001z~companycodeparametervalue AS billfrom_iecdt,
              adrc~region                     AS billfrom_statecode,
              t001z~companycodeparametervalue AS billfrom_cin,
              t001z~companycodeparametertype  AS party,
              zsdsupcodelut~suppliercode
              FROM @billingdata AS vbrkvbrp
              LEFT OUTER JOIN i_plant AS t001w ON t001w~plant = vbrkvbrp~werks
                                               AND t001w~language = @sy-langu
              LEFT OUTER JOIN i_addrorgnamepostaladdress WITH PRIVILEGED ACCESS AS adrc ON adrc~addressid = t001w~addressid
              LEFT OUTER JOIN i_regiontext AS t005u ON  t005u~region = adrc~region
                                                    AND t005u~country = adrc~country
                                                    AND t005u~language = @sy-langu
              LEFT OUTER JOIN j_1bbranch ON j_1bbranch~branch = vbrkvbrp~bupla
              LEFT OUTER JOIN i_addlcompanycodeinformation AS t001z ON vbrkvbrp~bukrs = t001z~companycode
              LEFT OUTER JOIN zsdsupcodelut ON zsdsupcodelut~customerno = vbrkvbrp~kunag
              WHERE vbrkvbrp~vbeln = @billingdocument INTO TABLE @DATA(billfrom).

        IF billfrom IS NOT INITIAL.
          ASSIGN billfrom[ vbeln = billingdocument ] TO FIELD-SYMBOL(<fs_billfrom>). "#EC CI_STDSEQ
          IF <fs_billfrom> IS ASSIGNED.
            er_entity-billfromaddress = condense( COND #( WHEN <fs_billfrom>-billfrom_name1 IS NOT INITIAL
                                                          THEN <fs_billfrom>-billfrom_name1 ) ).

            er_entity-billfromaddress = condense( COND #( WHEN er_entity-billfromaddress IS NOT INITIAL AND <fs_billfrom>-billfrom_name2 IS NOT INITIAL
                                                          THEN |{ er_entity-billfromaddress }{ <fs_billfrom>-billfrom_name2 }|
                                                          WHEN er_entity-billfromaddress IS INITIAL AND <fs_billfrom>-billfrom_name2 IS NOT INITIAL
                                                          THEN |{ <fs_billfrom>-billfrom_name2 }|
                                                          WHEN er_entity-billfromaddress IS NOT INITIAL AND <fs_billfrom>-billfrom_name2 IS INITIAL
                                                          THEN |{ er_entity-billfromaddress }| ) ).

            er_entity-billfromaddress = condense( COND #( WHEN er_entity-billfromaddress IS NOT INITIAL AND <fs_billfrom>-billfrom_street IS NOT INITIAL
                                                          THEN |{ er_entity-billfromaddress }{ cl_abap_char_utilities=>newline }{ <fs_billfrom>-billfrom_street }|
                                                          WHEN er_entity-billfromaddress IS INITIAL AND <fs_billfrom>-billfrom_street IS NOT INITIAL
                                                          THEN |{ <fs_billfrom>-billfrom_street }|
                                                          WHEN er_entity-billfromaddress IS NOT INITIAL AND <fs_billfrom>-billfrom_street IS INITIAL
                                                          THEN |{ er_entity-billfromaddress }| ) ).

            er_entity-billfromaddress = condense( COND #( WHEN er_entity-billfromaddress IS NOT INITIAL AND <fs_billfrom>-billfrom_city1 IS NOT INITIAL
                                                          THEN |{ er_entity-billfromaddress }{ cl_abap_char_utilities=>newline }{ <fs_billfrom>-billfrom_city1 }|
                                                          WHEN er_entity-billfromaddress IS INITIAL AND <fs_billfrom>-billfrom_city1 IS NOT INITIAL
                                                          THEN |{ <fs_billfrom>-billfrom_city1 }|
                                                          WHEN er_entity-billfromaddress IS NOT INITIAL AND <fs_billfrom>-billfrom_city1 IS INITIAL
                                                          THEN |{ er_entity-billfromaddress }| ) ).

            er_entity-billfromaddress = condense( COND #( WHEN er_entity-billfromaddress IS NOT INITIAL AND <fs_billfrom>-billfrom_postcode IS NOT INITIAL
                                                          THEN |{ er_entity-billfromaddress } - { <fs_billfrom>-billfrom_postcode }|
                                                          WHEN er_entity-billfromaddress IS INITIAL AND <fs_billfrom>-billfrom_postcode IS NOT INITIAL
                                                          THEN |{ <fs_billfrom>-billfrom_postcode }|
                                                          WHEN er_entity-billfromaddress IS NOT INITIAL AND <fs_billfrom>-billfrom_postcode IS INITIAL
                                                          THEN |{ er_entity-billfromaddress }| ) ).

            er_entity-billfromstatecode =  condense( |{ COND #( WHEN <fs_billfrom>-billfrom_statecode IS NOT INITIAL AND <fs_billfrom>-billfrom_regiondescription IS NOT INITIAL
                                                                THEN |{ <fs_billfrom>-billfrom_statecode } - { <fs_billfrom>-billfrom_regiondescription }| ) }{
                                                        COND #( WHEN <fs_billfrom>-billfrom_statecode IS NOT INITIAL AND <fs_billfrom>-billfrom_regiondescription IS INITIAL
                                                                THEN |{ <fs_billfrom>-billfrom_statecode }| ) }{
                                                        COND #( WHEN <fs_billfrom>-billfrom_statecode IS INITIAL AND <fs_billfrom>-billfrom_regiondescription IS NOT INITIAL
                                                                THEN |{ <fs_billfrom>-billfrom_regiondescription }| ) }| ).

*            er_entity-billfromstatecode = <fs_billfrom>-billfrom_statecode.
            er_entity-billfromplant     = <fs_billfrom>-billfrom_plant.
            er_entity-billfromgst       = <fs_billfrom>-billfrom_gstin.
            er_entity-billfromsuppcode  = <fs_billfrom>-suppliercode.

          ENDIF.
          UNASSIGN <fs_billfrom>.
          er_entity-billfromcin = VALUE #( billfrom[ vbeln = billingdocument party = 'CIN' ]-billfrom_cin OPTIONAL ).
          er_entity-billfromiec = VALUE #( billfrom[ vbeln = billingdocument party = 'IEC' ]-billfrom_iec OPTIONAL ).
          er_entity-billfromiecdt = VALUE #( billfrom[ vbeln = billingdocument party = 'IECDT' ]-billfrom_iecdt OPTIONAL ).
          er_entity-billfrompan = VALUE #( billfrom[ vbeln = billingdocument party = 'J_1I02' ]-billfrom_pan OPTIONAL ).

          suppliercode = er_entity-billfromsuppcode.
        ENDIF.

        " Fetching Data for Billing To Address Details
        SELECT
              vbrkvbrp~vbeln      AS vbeln,
              vbrkvbrp~kunag      AS billto_customercode,
              adrc~addresseename1 AS billto_name1,
              adrc~addresseename2 AS billto_name2,
              adrc~streetname     AS billto_street,
              adrc~cityname       AS billto_city1,
              adrc~country        AS billto_country,
              adrc~postalcode     AS billto_postcode,
              t005u~bezei         AS billto_regiondescription,
              dfkkbptaxnum~taxnum AS billto_gstin,
              dfkkbptaxnum~taxtype,
              kna1~j_1ipanno      AS billto_pan,
              kna1~regio         AS billto_statecode          FROM @billingdata AS vbrkvbrp
                                  LEFT OUTER JOIN kna1         ON kna1~kunnr   = vbrkvbrp~kunag
                                  LEFT OUTER JOIN i_addrorgnamepostaladdress WITH PRIVILEGED ACCESS AS adrc  ON adrc~addressid = kna1~adrnr
                                  LEFT OUTER JOIN t005u        ON t005u~bland          = adrc~region
                                                               AND t005u~land1         = adrc~country
                                                               AND t005u~spras         = @sy-langu
                                  LEFT OUTER JOIN dfkkbptaxnum ON dfkkbptaxnum~partner = vbrkvbrp~kunag
                                  WHERE vbrkvbrp~vbeln = @billingdocument
                                  INTO TABLE @DATA(billto).
        IF billto IS NOT INITIAL.
          ASSIGN billto[ vbeln = billingdocument ] TO FIELD-SYMBOL(<fs_billto>). "#EC CI_STDSEQ
          IF <fs_billto> IS ASSIGNED.
            er_entity-billtoaddress = condense( COND #( WHEN <fs_billto>-billto_name1 IS NOT INITIAL
                                                        THEN <fs_billto>-billto_name1 ) ).

            er_entity-billtoaddress = condense( COND #( WHEN er_entity-billtoaddress IS NOT INITIAL AND <fs_billto>-billto_name2 IS NOT INITIAL
                                                          THEN |{ er_entity-billtoaddress }{ <fs_billto>-billto_name2 }|
                                                          WHEN er_entity-billtoaddress IS INITIAL AND <fs_billto>-billto_name2 IS NOT INITIAL
                                                          THEN |{ <fs_billto>-billto_name2 }|
                                                          WHEN er_entity-billtoaddress IS NOT INITIAL AND <fs_billto>-billto_name2 IS INITIAL
                                                          THEN |{ er_entity-billtoaddress }| ) ).

            er_entity-billtoaddress = condense( COND #( WHEN er_entity-billtoaddress IS NOT INITIAL AND <fs_billto>-billto_street IS NOT INITIAL
                                                        THEN |{ er_entity-billtoaddress }{ cl_abap_char_utilities=>newline }{ <fs_billto>-billto_street }|
                                                        WHEN er_entity-billtoaddress IS INITIAL AND <fs_billto>-billto_street IS NOT INITIAL
                                                        THEN |{ <fs_billto>-billto_street }|
                                                        WHEN er_entity-billtoaddress IS NOT INITIAL AND <fs_billto>-billto_street IS INITIAL
                                                        THEN |{ er_entity-billtoaddress }| ) ).

            er_entity-billtoaddress = condense( COND #( WHEN er_entity-billtoaddress IS NOT INITIAL AND <fs_billto>-billto_city1 IS NOT INITIAL
                                                        THEN |{ er_entity-billtoaddress }{ cl_abap_char_utilities=>newline }{ <fs_billto>-billto_city1 }|
                                                        WHEN er_entity-billtoaddress IS INITIAL AND <fs_billto>-billto_city1 IS NOT INITIAL
                                                        THEN |{ <fs_billto>-billto_city1 }|
                                                        WHEN er_entity-billtoaddress IS NOT INITIAL AND <fs_billto>-billto_city1 IS INITIAL
                                                        THEN |{ er_entity-billtoaddress }| ) ).

            er_entity-billtoaddress = condense( COND #( WHEN er_entity-billtoaddress IS NOT INITIAL AND <fs_billto>-billto_postcode IS NOT INITIAL
                                                        THEN |{ er_entity-billtoaddress } - { <fs_billto>-billto_postcode }|
                                                        WHEN er_entity-billtoaddress IS INITIAL AND <fs_billto>-billto_postcode IS NOT INITIAL
                                                        THEN |{ <fs_billto>-billto_postcode }|
                                                        WHEN er_entity-billtoaddress IS NOT INITIAL AND <fs_billto>-billto_postcode IS INITIAL
                                                        THEN |{ er_entity-billtoaddress }| ) ).

            er_entity-billtostatecode  =  condense( |{ COND #( WHEN <fs_billto>-billto_statecode IS NOT INITIAL AND <fs_billto>-billto_regiondescription IS NOT INITIAL
                                                             THEN |{ <fs_billto>-billto_statecode } - { <fs_billto>-billto_regiondescription }| ) }{
                                                     COND #( WHEN <fs_billto>-billto_statecode IS NOT INITIAL AND <fs_billto>-billto_regiondescription IS INITIAL
                                                             THEN |{ <fs_billto>-billto_statecode }| ) }{
                                                     COND #( WHEN <fs_billto>-billto_statecode IS INITIAL AND <fs_billto>-billto_regiondescription IS NOT INITIAL
                                                             THEN |{ <fs_billto>-billto_regiondescription }| ) }| ).
            er_entity-billtocustomercode = <fs_billto>-billto_customercode.
            er_entity-billtopan          = <fs_billto>-billto_pan.
          ENDIF.
          UNASSIGN <fs_billto>.
          er_entity-billtogst           = VALUE #( billto[ vbeln = billingdocument taxtype = 'IN3' ]-billto_gstin OPTIONAL ).
        ENDIF.

**********************************************************************************************
        " Fetching Ship from Address details
        SELECT
                      vbrkvbrp~vbeln       AS vbeln,
                      t001z~paval          AS shipfrom_iec,
                      t001z~paval          AS shipfrom_iecdt,
                      t001z~paval          AS shipfrom_cin,
                      t001z~paval          AS shipfrom_pan,
                      t001z~party          AS party,
                      _adrc~addresseename1 AS shipfrom_name1,
                      _adrc~addresseename2 AS shipfrom_name2,
                      _adrc~streetname     AS shipfrom_street,
                      _adrc~cityname       AS shipfrom_city1,
                      _adrc~districtname   AS shipfrom_city2,
                      _adrc~region         AS shipfrom_statecode,
                      _adrc~country        AS shipfrom_country,
                      _adrc~postalcode     AS shipfrom_postcode,
                      t005u~bezei          AS shipfrom_regiondescription,
                      vbrkvbrp~zz1_shipfrom_bdh AS shipfrom_plant
                                       FROM @billingdata            AS vbrkvbrp
                                       LEFT OUTER JOIN t001w        ON t001w~werks = vbrkvbrp~zz1_shipfrom_bdh
                                       LEFT OUTER JOIN i_addrorgnamepostaladdress WITH PRIVILEGED ACCESS AS _adrc ON _adrc~addressid  = t001w~adrnr
                                       LEFT OUTER JOIN t001z        ON vbrkvbrp~bukrs  = t001z~bukrs
                                       LEFT OUTER JOIN kna1         ON kna1~kunnr = vbrkvbrp~zz1_shipfrom_bdh
*                                       LEFT OUTER JOIN i_addrorgnamepostaladdress WITH PRIVILEGED ACCESS AS adrc ON adrc~addressid   = kna1~adrnr
                                       LEFT OUTER JOIN t005u        ON t005u~bland     = _adrc~region
                                                                    AND t005u~land1    = _adrc~country
                                                                    AND t005u~spras    = @sy-langu
                                       WHERE vbrkvbrp~vbeln = @billingdocument
                                       INTO TABLE @DATA(shipfrom).

        " Fetching Data for Ship From Address Details
        ASSIGN shipfrom[ vbeln = billingdocument ] TO FIELD-SYMBOL(<fs_shipfrom>) . "DP
        IF <fs_shipfrom> IS ASSIGNED.
*
          er_entity-shipfromaddress = condense( COND #( WHEN <fs_shipfrom>-shipfrom_name1 IS NOT INITIAL
                                                        THEN <fs_shipfrom>-shipfrom_name1 ) ).

          er_entity-shipfromaddress = condense( COND #( WHEN er_entity-shipfromaddress IS NOT INITIAL AND <fs_shipfrom>-shipfrom_name2 IS NOT INITIAL
                                                        THEN |{ er_entity-shipfromaddress }{ <fs_shipfrom>-shipfrom_name2 }|
                                                        WHEN er_entity-shipfromaddress IS INITIAL AND <fs_shipfrom>-shipfrom_name2 IS NOT INITIAL
                                                        THEN |{ <fs_shipfrom>-shipfrom_name2 }|
                                                        WHEN er_entity-shipfromaddress IS NOT INITIAL AND <fs_shipfrom>-shipfrom_name2 IS INITIAL
                                                        THEN |{ er_entity-shipfromaddress }| ) ).

          er_entity-shipfromaddress = condense( COND #( WHEN er_entity-shipfromaddress IS NOT INITIAL AND <fs_shipfrom>-shipfrom_street IS NOT INITIAL
                                                      THEN |{ er_entity-shipfromaddress }{ cl_abap_char_utilities=>newline }{ <fs_shipfrom>-shipfrom_street }|
                                                      WHEN er_entity-shipfromaddress IS INITIAL AND <fs_shipfrom>-shipfrom_street IS NOT INITIAL
                                                      THEN |{ <fs_shipfrom>-shipfrom_street }|
                                                      WHEN er_entity-shipfromaddress IS NOT INITIAL AND <fs_shipfrom>-shipfrom_street IS INITIAL
                                                      THEN |{ er_entity-shipfromaddress }| ) ).

          er_entity-shipfromaddress = condense( COND #( WHEN er_entity-shipfromaddress IS NOT INITIAL AND <fs_shipfrom>-shipfrom_city1 IS NOT INITIAL
                                                      THEN |{ er_entity-shipfromaddress }{ cl_abap_char_utilities=>newline }{ <fs_shipfrom>-shipfrom_city1 }|
                                                      WHEN er_entity-shipfromaddress IS INITIAL AND <fs_shipfrom>-shipfrom_city1 IS NOT INITIAL
                                                      THEN |{ <fs_shipfrom>-shipfrom_city1 }|
                                                      WHEN er_entity-shipfromaddress IS NOT INITIAL AND <fs_shipfrom>-shipfrom_city1 IS INITIAL
                                                      THEN |{ er_entity-shipfromaddress }| ) ).

          er_entity-shipfromaddress = condense( COND #( WHEN er_entity-shipfromaddress IS NOT INITIAL AND <fs_shipfrom>-shipfrom_postcode IS NOT INITIAL
                                                      THEN |{ er_entity-shipfromaddress } - { <fs_shipfrom>-shipfrom_postcode }|
                                                      WHEN er_entity-shipfromaddress IS INITIAL AND <fs_shipfrom>-shipfrom_postcode IS NOT INITIAL
                                                      THEN |{ <fs_shipfrom>-shipfrom_postcode }|
                                                      WHEN er_entity-shipfromaddress IS NOT INITIAL AND <fs_shipfrom>-shipfrom_postcode IS INITIAL
                                                      THEN |{ er_entity-shipfromaddress }| ) ).

          er_entity-shipfromstatecode = condense( |{ COND #( WHEN <fs_shipfrom>-shipfrom_statecode IS NOT INITIAL AND <fs_shipfrom>-shipfrom_regiondescription IS NOT INITIAL
                                                            THEN |{ <fs_shipfrom>-shipfrom_statecode } - { <fs_shipfrom>-shipfrom_regiondescription }| ) }{
                                                    COND #( WHEN <fs_shipfrom>-shipfrom_statecode IS NOT INITIAL AND <fs_shipfrom>-shipfrom_regiondescription IS INITIAL
                                                            THEN |{ <fs_shipfrom>-shipfrom_statecode }| ) }{
                                                    COND #( WHEN <fs_shipfrom>-shipfrom_statecode IS INITIAL AND <fs_shipfrom>-shipfrom_regiondescription IS NOT INITIAL
                                                            THEN |{ <fs_shipfrom>-shipfrom_regiondescription }| ) }| ).

          er_entity-shipfromplant     = VALUE #( shipfrom[ vbeln = billingdocument ]-shipfrom_plant OPTIONAL ).
          er_entity-shipfrompan       = VALUE #( shipfrom[ vbeln = billingdocument party = 'J_1I02' ]-shipfrom_pan OPTIONAL ).
          er_entity-shipfromiec       = VALUE #( shipfrom[ vbeln = billingdocument party = 'IEC'    ]-shipfrom_iec OPTIONAL ).
          er_entity-shipfromiecdt     = VALUE #( shipfrom[ vbeln = billingdocument party = 'IECDT'  ]-shipfrom_iecdt OPTIONAL ).
          er_entity-shipfromcin       = VALUE #( shipfrom[ vbeln = billingdocument party = 'CIN'  ]-shipfrom_cin OPTIONAL ).
          UNASSIGN <fs_shipfrom>.
        ENDIF.

        SELECT   vbeln,
                 zz1_shipfrom_bdh FROM vbrk INTO TABLE @DATA(vbrk)
                  WHERE vbeln = @billingdocument.

        gst = VALUE #(
          FOR gsttable IN vbrk
          ( sign   = /isdfps/cl_const_abc_123=>gc_i
            option =  |{ /isdfps/cl_const_abc_123=>gc_e && /isdfps/cl_const_abc_123=>gc_q }|
            low    = |{ gsttable-zz1_shipfrom_bdh ALPHA = IN }| ) ).

        SELECT taxnum ,
               taxtype,
               partner FROM dfkkbptaxnum INTO TABLE @DATA(gstinno)
               WHERE taxtype = 'IN3' AND partner IN @gst.

        er_entity-shipfromgst       = VALUE #( gstinno[ taxtype = 'IN3'  ]-taxnum OPTIONAL ).

        " Fetching Data for Ship To Address Details
        SELECT
              vbrkvbrp~vbeln       AS vbeln,
              vbpa~kunnr       AS kunnr,
              vbpa~assigned_bp     AS shipto_plant,
              adrc~addresseename1  AS shipto_name1,
              adrc~addresseename2  AS shipto_name2,
              adrc~streetname      AS shipto_street,
              adrc~cityname        AS shipto_city1,
              adrc~country         AS shipto_country,
              adrc~postalcode      AS shipto_postcode,
              t005u~bezei          AS shipto_regiondescription,
              vbrkvbrp~kunag           AS shipto_customercode,
              dfkkbptaxnum~taxnum  AS shipto_gstin,
              dfkkbptaxnum~taxtype,
              kna1~j_1ipanno       AS shipto_pan,
              adrc~region          AS shipto_statecode,
              kna1~regio           AS shipto_suppliercode,
              t001z~paval          AS shipto_cin,
              t001z~party          AS party,
              vbpa~parvw,
               vbrkvbrp~zz1_shipfrom_bdh
                               FROM @billingdata            AS vbrkvbrp
                               LEFT OUTER JOIN vbpa         ON vbpa~vbeln       = vbrkvbrp~vbeln
                                                            AND vbpa~parvw IN ( 'WE' ) "SH = WE
                               LEFT OUTER JOIN i_addrorgnamepostaladdress WITH PRIVILEGED ACCESS AS adrc ON adrc~addressid   = vbpa~adrnr
                               LEFT OUTER JOIN t005u        ON t005u~bland       = adrc~region
                                                            AND t005u~land1      = adrc~country
                                                            AND t005u~spras      = @sy-langu
                               LEFT OUTER JOIN dfkkbptaxnum ON dfkkbptaxnum~partner = vbpa~kunnr
                               LEFT OUTER JOIN t001z        ON vbrkvbrp~bukrs     = t001z~bukrs
                               LEFT OUTER JOIN kna1         ON vbrkvbrp~kunwe     = kna1~kunnr
                               WHERE vbrkvbrp~vbeln = @billingdocument
                               INTO TABLE @DATA(ship).
        IF ship IS NOT INITIAL.

          " Fetching Data for Ship To Address Details "SH
          ASSIGN ship[ vbeln = billingdocument parvw = 'WE' ] TO FIELD-SYMBOL(<fs_shipto>). "#EC CI_STDSEQ
          IF <fs_shipto> IS ASSIGNED.

            er_entity-shiptoaddress = condense( COND #( WHEN <fs_shipto>-shipto_name1 IS NOT INITIAL
                                                        THEN <fs_shipto>-shipto_name1 ) ).

            er_entity-shiptoaddress = condense( COND #( WHEN er_entity-shiptoaddress IS NOT INITIAL AND <fs_shipto>-shipto_name2 IS NOT INITIAL
                                                          THEN |{ er_entity-shiptoaddress }{ <fs_shipto>-shipto_name2 }|
                                                          WHEN er_entity-shiptoaddress IS INITIAL AND <fs_shipto>-shipto_name2 IS NOT INITIAL
                                                          THEN |{ <fs_shipto>-shipto_name2 }|
                                                          WHEN er_entity-shiptoaddress IS NOT INITIAL AND <fs_shipto>-shipto_name2 IS INITIAL
                                                          THEN |{ er_entity-shiptoaddress }| ) ).

            er_entity-shiptoaddress = condense( COND #( WHEN er_entity-shiptoaddress IS NOT INITIAL AND <fs_shipto>-shipto_street IS NOT INITIAL
                                                        THEN |{ er_entity-shiptoaddress }{ cl_abap_char_utilities=>newline }{ <fs_shipto>-shipto_street }|
                                                        WHEN er_entity-shiptoaddress IS INITIAL AND <fs_shipto>-shipto_street IS NOT INITIAL
                                                        THEN |{ <fs_shipto>-shipto_street }|
                                                        WHEN er_entity-shiptoaddress IS NOT INITIAL AND <fs_shipto>-shipto_street IS INITIAL
                                                        THEN |{ er_entity-shiptoaddress }| ) ).

            er_entity-shiptoaddress = condense( COND #( WHEN er_entity-shiptoaddress IS NOT INITIAL AND <fs_shipto>-shipto_city1 IS NOT INITIAL
                                                        THEN |{ er_entity-shiptoaddress }{ cl_abap_char_utilities=>newline }{ <fs_shipto>-shipto_city1 }|
                                                        WHEN er_entity-shiptoaddress IS INITIAL AND <fs_shipto>-shipto_city1 IS NOT INITIAL
                                                        THEN |{ <fs_shipto>-shipto_city1 }|
                                                        WHEN er_entity-shiptoaddress IS NOT INITIAL AND <fs_shipto>-shipto_city1 IS INITIAL
                                                        THEN |{ er_entity-shiptoaddress }| ) ).

            er_entity-shiptoaddress = condense( COND #( WHEN er_entity-shiptoaddress IS NOT INITIAL AND <fs_shipto>-shipto_postcode IS NOT INITIAL
                                                        THEN |{ er_entity-shiptoaddress } - { <fs_shipto>-shipto_postcode }|
                                                        WHEN er_entity-shiptoaddress IS INITIAL AND <fs_shipto>-shipto_postcode IS NOT INITIAL
                                                        THEN |{ <fs_shipto>-shipto_postcode }|
                                                        WHEN er_entity-shiptoaddress IS NOT INITIAL AND <fs_shipto>-shipto_postcode IS INITIAL
                                                        THEN |{ er_entity-shiptoaddress }| ) ).

            er_entity-shiptostatecode  = condense( |{ COND #( WHEN <fs_shipto>-shipto_statecode IS NOT INITIAL AND <fs_shipto>-shipto_regiondescription IS NOT INITIAL
                                                              THEN |{ <fs_shipto>-shipto_statecode } - { <fs_shipto>-shipto_regiondescription }| ) }{
                                                      COND #( WHEN <fs_shipto>-shipto_statecode IS NOT INITIAL AND <fs_shipto>-shipto_regiondescription IS INITIAL
                                                              THEN |{ <fs_shipto>-shipto_statecode }| ) }{
                                                      COND #( WHEN <fs_shipto>-shipto_statecode IS INITIAL AND <fs_shipto>-shipto_regiondescription IS NOT INITIAL
                                                              THEN |{ <fs_shipto>-shipto_regiondescription }| ) }| ).
          ENDIF.
          UNASSIGN <fs_shipto>.

          er_entity-shiptocustomercode =  VALUE #( ship[ vbeln = billingdocument ]-shipto_customercode OPTIONAL ).
          er_entity-shiptogst          =  VALUE #( ship[ vbeln = billingdocument taxtype = 'IN3'  ]-shipto_gstin OPTIONAL ).
          er_entity-shiptopan          =  VALUE #( ship[ vbeln = billingdocument party = 'J_1I02' ]-shipto_pan OPTIONAL ).
          er_entity-shiptocin          =  VALUE #( ship[ vbeln = billingdocument taxtype = 'CIN'  ]-shipto_cin OPTIONAL ).
        ENDIF.

        " Start of changes from 05/12/2025
        SELECT SINGLE
                      vbrkvbrp~vbeln,
                      vbrkvbrp~zz1_transportvendorco_bdh     AS zz1_transportvendorco_bdh,
                      vbrkvbrp~zz1_vendorgstinnumber_bdh     AS transporter_gstin,
                      vbrkvbrp~zz1_transportvendorgst_bdh    AS transporter_name
                                  FROM @billingdata AS vbrkvbrp WHERE vbrkvbrp~vbeln = @billingdocument
                                       INTO @DATA(vendor_det).
        IF sy-subrc = 0.
          er_entity-vendorcode = vendor_det-zz1_transportvendorco_bdh.
          IF  er_entity-vendorcode IS INITIAL.
            er_entity-transportername  = vendor_det-transporter_name.
            er_entity-transportergstin = vendor_det-transporter_gstin.
          ENDIF.
        ENDIF.
        " End of changes from 05/12/2025

        " Fetching Data for Vendor Details
        SELECT
                  vbrkvbrp~vbeln                         AS vbeln,
                  vbrkvbrp~zz1_transportvendorco_bdh     AS zz1_transportvendorco_bdh,
                  adrc~addresseename1                    AS transporter_name,
                  dfkkbptaxnum~taxnum                    AS transporter_gstin,
                  dfkkbptaxnum~taxtype                   AS taxtype
                                      FROM @billingdata AS vbrkvbrp
                                      LEFT OUTER JOIN lfa1 ON lfa1~lifnr = vbrkvbrp~zz1_transportvendorco_bdh
                                      LEFT OUTER JOIN i_addrorgnamepostaladdress WITH PRIVILEGED ACCESS AS adrc ON adrc~addressid = lfa1~adrnr
                                      LEFT OUTER JOIN dfkkbptaxnum ON dfkkbptaxnum~partner = vbrkvbrp~zz1_transportvendorco_bdh
                                                                  " AND dfkkbptaxnum~taxtype = 'IN3'
                                      WHERE vbrkvbrp~vbeln = @billingdocument
                                      INTO TABLE @DATA(vendor_details).
        IF vendor_details IS NOT INITIAL.
          ASSIGN vendor_details[ vbeln = billingdocument ] TO FIELD-SYMBOL(<vendor>). "#EC CI_STDSEQ
          IF <vendor> IS ASSIGNED.
            IF  er_entity-vendorcode IS NOT INITIAL.
*            er_entity-vendorcode = <vendor>-zz1_transportvendorco_bdh.
              er_entity-transportername = <vendor>-transporter_name.
*            er_entity-transportergstin =  condense( |{ COND #( WHEN <vendor>-taxtype = TEXT-004 "IN3
*                                                               THEN |{ <vendor>-transporter_gstin }| ) }| ).
              er_entity-transportergstin = <vendor>-transporter_gstin.
            ENDIF.
          ENDIF.
          UNASSIGN <vendor>.
        ENDIF.

        SELECT SINGLE
                      vbrkvbrp~vbeln                 AS vbeln,
                      vbrkvbrp~zz1_modeofdel_bdh     AS zz1_modeofdel_bdh,
                      vbrkvbrp~zz1_vehiclenumber_bdh AS zz1_vehiclenumber_bdh,
                      vbrkvbrp~zz1_vehicletype_bdh   AS zz1_vehicletype_bdh,
                      vbrkvbrp~zz1_distance_bdh      AS zz1_distance_bdh,
                      vbrkvbrp~zz1_lrnumber_bdh      AS zz1_lrnumber_bdh,
                      vbrkvbrp~zz1_lrdate_bdh        AS zz1_lrdate_bdh,
                      t173t~bezei                    AS mode_of_delivery
                      FROM @billingdata              AS vbrkvbrp
                      LEFT OUTER JOIN t173t ON t173t~vsart = vbrkvbrp~zz1_modeofdel_bdh
                                            AND t173t~spras = @sy-langu
                                            INTO @DATA(mode).
        IF mode IS NOT INITIAL.
          er_entity-modeofdelivery = mode-mode_of_delivery.
          er_entity-vehicleno      = mode-zz1_vehiclenumber_bdh.
          er_entity-vehicletype    = mode-zz1_vehicletype_bdh.
          er_entity-distance       = mode-zz1_distance_bdh.
          er_entity-lrdocketno     = mode-zz1_lrnumber_bdh.
          er_entity-lrdocketdate   = mode-zz1_lrdate_bdh.
        ENDIF.

        " Fetching LUT details in the footer level
        SELECT SINGLE
                vbrkvbrp~vbeln,
                zsdplantlut~lutno,
                zsdplantlut~lutdate,
                zsdplantlut~lutvalidity
                    FROM @billingdata AS vbrkvbrp
                    LEFT OUTER JOIN zsdplantlut AS zsdplantlut ON zsdplantlut~plant = vbrkvbrp~werks
                    WHERE vbrkvbrp~vbeln = @billingdocument
                    INTO @DATA(lutdetail).
        IF lutdetail IS NOT INITIAL.
          er_entity-lutno   = lutdetail-lutno.
          er_entity-lutdate = lutdetail-lutdate.
          er_entity-financialyear = lutdetail-lutvalidity.
        ENDIF.

        SELECT SINGLE
              vbrkvbrp~vbeln,
              vbrkvbrp~posnr,
              vbrkvbrp~aubel,
              vbrkvbrp~xblnr,
              vbfa~vbtyp_n,
              vbrk~fkdat,
              vbfa~vbelv,
              vbfa~vbeln AS vbel FROM @billingdata AS vbrkvbrp
              LEFT OUTER JOIN vbfa ON vbfa~vbelv = vbrkvbrp~aubel
              LEFT OUTER JOIN vbrk ON vbfa~vbeln = vbrk~vbeln
                                           WHERE vbrkvbrp~vbeln = @billingdocument
                                           AND vbfa~vbtyp_n = 'U'
                                           INTO @DATA(commercialdetail).
        IF commercialdetail IS NOT INITIAL.
          er_entity-commercialinvno = commercialdetail-xblnr.
          er_entity-commercialdate  = commercialdetail-fkdat.
        ENDIF.

        SELECT
              vbrkvbrp~vbeln,
              vbrkvbrp~aubel,
              vbap~auart_ana FROM @billingdata AS vbrkvbrp
              LEFT OUTER JOIN vbap ON vbap~vbeln = vbrkvbrp~aubel
              WHERE vbrkvbrp~vbeln = @billingdocument INTO TABLE @DATA(typeofexports).

        IF typeofexports IS NOT INITIAL.
          ASSIGN typeofexports[ vbeln = billingdocument ] TO FIELD-SYMBOL(<fs_typeexp>). "#EC CI_STDSEQ
          IF <fs_typeexp> IS ASSIGNED.
            er_entity-typeofexport = COND #( WHEN <fs_typeexp>-auart_ana = 'ZSE'
                                             THEN 'EXPWOP'
                                             WHEN <fs_typeexp>-auart_ana = 'ZSE1'
                                             THEN 'EXPWP'
                                             WHEN <fs_typeexp>-auart_ana = 'ZME'
                                             THEN 'Deemed Export' ).
            UNASSIGN <fs_typeexp>.
          ENDIF.
        ENDIF.

        DATA : rmk   TYPE thead-tdname.
        rmk = billingdocument.

        " Fetching Remarks
        yglobalutility=>readtext(
        EXPORTING
          iv_textid  =  'ZREM'             " Text ID
          iv_name    =   rmk               " Name
          iv_textobj =  'VBBK'             " Texts: application object
        IMPORTING
          ev_text    = DATA(remark) ).
        IF remark IS NOT INITIAL.
          er_entity-remarks = remark.
        ENDIF.

      ENDIF.
    ENDIF.
  ENDMETHOD.


  METHOD item_get_entity.
*----------------------------------------------------------------------*
* Class           ZCL_ZTAXINVOICE_DPC_EXT                              *
*----------------------------------------------------------------------*
* Title:          Dosmestic Tax Invoice                                *
* RICEF#:         RSB_SD_F_01                                          *
* Transaction:    VF01/VF02/VF03                                       *
*----------------------------------------------------------------------*
* Copyright:      NDBS, Inc.                                           *
* Client:         RSB Transmission                                     *
*----------------------------------------------------------------------*
* Developer:      NTT_ABAP5 ( Vaishnavi Vairagare )                    *
* Creation Date:  15/05/2025                                           *
* Description:    Domestic Tax Invoice                                 *
*----------------------------------------------------------------------*
* Modification History                                                 *
*----------------------------------------------------------------------*
* Modified by:    <Developer (full name and user name)>                *
* Date:           <Date>                                               *
* Transport:      <Transport Request #>                                *
* Description:                                                         *
*<Description of the change (or the source for the initial creation if *
* a template or SAP program was used as a starting point>              *
*----------------------------------------------------------------------*
    " Data Declaration For Billing Document Number.

    DATA(billingdocument) = VALUE #( it_key_tab[ name = 'BillingDocument' ]-value OPTIONAL ).

    " Data Declarations
*    DATA: itemdata          TYPE zcl_zexporttaxinv_mpc=>ts_itemdat001,
    DATA: itemdata          TYPE zcl_zexporttaxinv_mpc=>ts_itemdata,
          condition_type    TYPE RANGE OF prcd_elements-kschl,
          discounts         TYPE kbetr,
          igstper           TYPE p DECIMALS 1,
          sgstper           TYPE p DECIMALS 1,
          cgstper           TYPE p DECIMALS 1,
          tcsper            TYPE p DECIMALS 1,
          dis               TYPE p DECIMALS 2,
          tatol_basic_value TYPE p DECIMALS 2,
          qty_unit          TYPE netwr,
*          amtinwords        TYPE pc207-betrg,
*          invoiceamt        TYPE pc207-betrg,
          gstamt            TYPE char200,
          invamt            TYPE char200,
          totalbase         TYPE kbetr,
          exchangerate      TYPE vbrk-kurrf.

    "   Fetching ID's from TVARVC table
    SELECT
           name,
           low,
           high FROM tvarvc
                WHERE name = @text-001
                INTO TABLE @DATA(lt_tvarvc).            "#EC CI_NOORDER

    IF sy-subrc = 0.
      condition_type = VALUE #( FOR ls_tvarvc IN lt_tvarvc "#EC CI_STDSEQ
                              WHERE ( name = TEXT-001 ) "#EC CI_STDSEQ "ZMM_RFQ_TEXTIDS
                                    ( sign = |{ /isdfps/cl_const_abc_123=>gc_i }|
                                      option = |{ /isdfps/cl_const_abc_123=>gc_e && /isdfps/cl_const_abc_123=>gc_q }|
                                      low  = ls_tvarvc-low ) ).
    ENDIF.

    IF billingdata IS NOT INITIAL.
      SELECT
      billdata~vbeln,
      billdata~kurrf,
      billdata~posnr FROM @billingdata AS billdata
      WHERE vbeln = @billingdocument
      INTO TABLE @DATA(itemcount).

      SELECT billingdocument AS vbeln,
             totalnetamount  AS netwr FROM i_billingdocumentbasic AS _billdoc
                                      INTO TABLE @DATA(taxablevalue)
                                      WHERE _billdoc~billingdocument = @billingdocument.

      IF sy-subrc = 0.
      ENDIF.

      SELECT
            billdata~vbeln,
            billdata~posnr,
            billdata~fkart,
            billdata~kurrf,
            knvv~kvgr1 FROM @billingdata AS billdata
                       LEFT OUTER JOIN knvv ON  knvv~kunnr  = billdata~kunag
                                            AND knvv~vkorg = billdata~vkorg
                                            AND knvv~vtweg = billdata~vtweg
                                            AND knvv~spart = billdata~spart
                       WHERE vbeln = @billingdocument
                       AND knvv~kvgr1 = 'TML'
                       INTO TABLE @DATA(qrc).

      SELECT
            vbkd~bstkd,
            vbrkvbrp~aubel,
            vbrkvbrp~kurrf,
            vbrkvbrp~vbeln
        FROM @billingdata      AS vbrkvbrp
        LEFT OUTER JOIN vbkd  ON  vbrkvbrp~aubel = vbkd~vbeln
        INTO TABLE @DATA(lt_customer_qrc).

      SELECT vbrkvbrp~vbeln     AS vbeln,
             vbrkvbrp~posnr     AS posnr,
             vbrkvbrp~matnr     AS matnr,
             makt~maktx
             FROM @billingdata      AS vbrkvbrp
             LEFT OUTER JOIN makt   ON  vbrkvbrp~matnr = makt~matnr
                                    AND makt~spras = @sy-langu
                                    INTO TABLE @DATA(material_des).

      SELECT vbrkvbrp~vbeln     AS vbeln,
            vbrkvbrp~aubel     AS aubel,
            vbrkvbrp~werks     AS plant,
            vbrkvbrp~knumv_ana AS knumv_ana,
            vbrkvbrp~posnr     AS posnr,
            vbrkvbrp~matnr     AS material_code,
            vbrkvbrp~arktx     AS material_description,
            vbrkvbrp~vrkme     AS uom,
            vbrkvbrp~fkimg     AS quantity,
            vbrkvbrp~netwr     AS taxablevalue,
            vbrkvbrp~vkorg     AS vkorg,
            vbrkvbrp~fkdat,
            vbrkvbrp~kurrf,
            vbrkvbrp~kunag,
            vbap~kdmat         AS customer_material_code,
            vbrkvbrp~vtweg     AS vtweg FROM @billingdata  AS vbrkvbrp
            LEFT OUTER JOIN vbap ON vbap~vbeln = vbrkvbrp~aubel
            AND vbap~posnr = vbrkvbrp~posnr
            WHERE vbrkvbrp~vbeln = @billingdocument
       INTO TABLE @DATA(itemdetails).

      SELECT vbrkvbrp~vbeln AS vbeln,
             vbrkvbrp~kurrf AS kurrf,
             vbrkvbrp~matnr AS vbrp_matnr,
             vbrkvbrp~vkorg AS brk_vkorg,
             vbrkvbrp~vtweg AS vbrk_vtweg,
             vbrkvbrp~kunag AS vbrk_kunag,
             knmt~matnr,
             knmt~vkorg,
             knmt~vtweg,
             knmt~kunnr,
             knmt~postx          AS customermaterialdescription
            FROM @billingdata    AS vbrkvbrp
            LEFT OUTER JOIN knmt ON  vbrkvbrp~matnr = knmt~matnr
                                 AND vbrkvbrp~vkorg = knmt~vkorg
                                 AND vbrkvbrp~vtweg = knmt~vtweg
                                 AND vbrkvbrp~kunag = knmt~kunnr
            WHERE vbrkvbrp~vbeln = @billingdocument
            INTO TABLE @DATA(description).

      SELECT
            vbrkvbrp~vbeln AS vbeln,
            vbrkvbrp~matnr AS material,
            vbrkvbrp~werks AS plant,
            vbrkvbrp~kurrf,
            t604n~text1    AS hsn_description,
            marc~steuc     AS hsn_sac
            FROM @billingdata  AS vbrkvbrp
                    LEFT OUTER JOIN marc ON marc~matnr      = vbrkvbrp~matnr
                                            AND marc~werks     = vbrkvbrp~werks
                    LEFT OUTER JOIN t604n ON  marc~steuc    = t604n~steuc
                                          AND t604n~spras   = @sy-langu
                    WHERE vbrkvbrp~vbeln = @billingdocument
                    INTO TABLE @DATA(hsn).

      IF sy-subrc = 0.
      ENDIF.

      SELECT
        vbrkvbrp~vbeln AS vbeln,
        vbrkvbrp~posnr,
        vbrkvbrp~kurrf,
        vbrkvbrp~knumv_ana,
        prcd_elements~kposn,
        prcd_elements~knumv,
        prcd_elements~kbetr,
        prcd_elements~kschl,
        prcd_elements~kwert
            FROM @billingdata AS vbrkvbrp
            LEFT OUTER JOIN prcd_elements ON prcd_elements~kposn = vbrkvbrp~posnr
                                          AND prcd_elements~knumv  = vbrkvbrp~knumv_ana
                                          AND prcd_elements~kschl IN ( 'ZPR0' , 'ZBLK' , 'ZCDS' , 'ZBD1' , 'ZADC' , 'ZFLD' ,
                                                                       'ZFRE' , 'ZPAC' , 'ZTAC' , 'JOIG' , 'JOCG' , 'JOSG' ,
                                                                       'JTC2'  )
            WHERE vbrkvbrp~vbeln = @billingdocument
            INTO TABLE @DATA(pricing).

      DATA(posnr_count)  = lines( itemcount ).
      LOOP AT itemdetails ASSIGNING FIELD-SYMBOL(<fs_item>).
        itemdata-billingdocument             = <fs_item>-vbeln.
        exchangerate                         = <fs_item>-kurrf.
        IF posnr_count > 1.
          itemdata-emptyvalueqrc               = COND #( WHEN posnr_count > 1
                                                         THEN ''
                                                         ELSE 'X'  ) .
        ELSEIF posnr_count = 1.
          itemdata-emptyvalueqrc               = COND #( WHEN  VALUE #( qrc[ vbeln = <fs_item>-vbeln kvgr1 = 'TML' ]-kvgr1 OPTIONAL  ) = 'TML'
                                                         THEN 'X'
                                                         ELSE '' ).
        ENDIF.
        itemdata-materialcode                = |{ <fs_item>-material_code ALPHA = OUT }|.
        itemdata-materialcodedescrption      = VALUE #( material_des[ matnr = <fs_item>-material_code ]-maktx OPTIONAL ).
        itemdata-customermaterialcode        = <fs_item>-customer_material_code.
        itemdata-customermaterialdescription = VALUE #( description[ matnr = <fs_item>-material_code
                                                                     kunnr = <fs_item>-kunag
                                                                     vkorg = <fs_item>-vkorg
                                                                     vtweg = <fs_item>-vtweg ]-customermaterialdescription OPTIONAL ).
        itemdata-hsnsac                      = VALUE #( hsn[ material = <fs_item>-material_code
                                                             plant = <fs_item>-plant ]-hsn_sac OPTIONAL ).
        itemdata-hsndescription              = VALUE #( hsn[ material = <fs_item>-material_code
                                                             plant = <fs_item>-plant ]-hsn_description OPTIONAL ).
        itemdata-quntity                     = <fs_item>-quantity.

        IF <fs_item>-uom IS NOT INITIAL.
          CALL FUNCTION 'CONVERSION_EXIT_CUNIT_OUTPUT'
            EXPORTING
              input          = <fs_item>-uom
              language       = sy-langu
            IMPORTING
*             LONG_TEXT      =
              output         = <fs_item>-uom
*             SHORT_TEXT     =
            EXCEPTIONS
              unit_not_found = 1
              OTHERS         = 2.
          IF sy-subrc <> 0.
* Implement suitable error handling here
          ENDIF.
        ENDIF.

        itemdata-uom                         = <fs_item>-uom.
        itemdata-unitprise                   =  VALUE #( pricing[ kposn = <fs_item>-posnr kschl = 'ZPR0' ]-kbetr OPTIONAL ) * exchangerate.
        qty_unit                             = itemdata-quntity * itemdata-unitprise.
        discounts                            =  REDUCE vfprc_element_amount( INIT lv_dist TYPE vfprc_element_amount "#EC CI_STDSEQ
                                                                            FOR ls_pricing IN pricing
                                                                            WHERE ( knumv = <fs_item>-knumv_ana
                                                                            AND kposn = <fs_item>-posnr
                                                                            AND kschl IN condition_type )
                                                NEXT lv_dist = lv_dist + ls_pricing-kbetr ) * ( -1 ).. " / 1000.

        itemdata-discount                    = |{ discounts }{ '%' }|.
        dis                                  = ( discounts / 100 ) * itemdata-unitprise.
        itemdata-discvalue                   = qty_unit * ( discounts / 100 ).
        itemdata-valueafterdiscount          = qty_unit - itemdata-discvalue.
        itemdata-value2                      = itemdata-quntity * itemdata-unitprise.
        itemdata-emptyvalue                  = COND #( WHEN discounts = '0.0' OR itemdata-discvalue = '0.0%'
                                                       THEN ''
                                                       ELSE 'X' ).
        itemdata-tatolbasicvalue             = REDUCE vfprc_element_value( INIT lv_totalbasic TYPE vfprc_element_value "#EC CI_STDSEQ
                                                                           FOR ls_pricing IN pricing
                                                                           WHERE ( vbeln = billingdocument
                                                                           AND knumv_ana = <fs_item>-knumv_ana
                                                                           AND kposn = <fs_item>-posnr
                                                                           AND kschl = 'ZPR0' )
                                               NEXT lv_totalbasic = ls_pricing-kwert ) * exchangerate.
        itemdata-customerqrc                 = billingdocument.
        APPEND itemdata TO et_entityset.
        CLEAR : itemdata,
                qty_unit.
      ENDLOOP.

      " Amount in words for GST
*      amtinwords =  itemdata-igstvaluetot +  itemdata-cgstvaluetot +  itemdata-sgstvaluetot +  itemdata-tcsvaluetot.

      " Amount in words for Total GST
      yglobalutility=>amountinwords(
        EXPORTING
          iv_amt_in_num   = amtinwords                 " HR Payroll: Amount
        IMPORTING
          ev_amt_in_words = gstamt
      ).

      IF sy-subrc = 0.
        CONDENSE gstamt.
        DATA gst_amt TYPE string.
        gst_amt = gstamt.
        TRANSLATE gst_amt TO LOWER CASE.
        gst_amt = cl_hrpayus_format_string=>conv_first_chars_to_upper_case( gst_amt ).
        gst_amt = |{ gst_amt }|.
      ENDIF.

      IF taxablevalue IS NOT INITIAL.
        itemdata-taxablevalue = VALUE #( taxablevalue[ vbeln = billingdocument ]-netwr OPTIONAL ).
        DATA(taxable) = itemdata-taxablevalue.
      ENDIF.

*      "Amount in words for Total Invoice value
*      invoiceamt = itemdata-taxablevalue + amtinwords.

      yglobalutility=>amountinwords(
              EXPORTING
                iv_amt_in_num   = invoiceamt                 " HR Payroll: Amount
              IMPORTING
                ev_amt_in_words = invamt
            ).

      IF sy-subrc = 0.
        CONDENSE invamt.
        DATA inv_amt TYPE string.
        inv_amt = invamt.
        TRANSLATE inv_amt TO LOWER CASE.
        inv_amt = cl_hrpayus_format_string=>conv_first_chars_to_upper_case( inv_amt ).
        inv_amt = |{ inv_amt }|.
      ENDIF.

      itemdata-totalbasic = REDUCE fkimg( INIT lv_bas TYPE fkimg "#EC CI_STDSEQ
                                              FOR ls_entityset IN et_entityset
                            NEXT lv_bas = lv_bas + ls_entityset-tatolbasicvalue ) .

      MODIFY et_entityset FROM VALUE #( igsttot      = itemdata-igsttot
                                        igstvaluetot = itemdata-igstvaluetot
                                        cgsttot      = itemdata-cgsttot
                                        cgstvaluetot = itemdata-cgstvaluetot
                                        sgsttot      = itemdata-sgsttot
                                        sgstvaluetot = itemdata-sgstvaluetot
                                        tcstot       = itemdata-tcstot
                                        tcsvaluetot  = itemdata-tcsvaluetot
                                        totalinvoicevalue =  invoiceamt
                                        invamtwords    = inv_amt
                                        gstamtwords    = gst_amt
                                        totalbasic     = itemdata-totalbasic
                                        taxablevalue   = itemdata-taxablevalue  )

      TRANSPORTING igsttot igstvaluetot  cgsttot            cgstvaluetot
                   sgsttot sgstvaluetot  taxablevalue       gstamtwords
                   tcstot  tcsvaluetot   totalinvoicevalue  totalbasic  invamtwords
      WHERE billingdocument IS NOT INITIAL.
    ENDIF.
  ENDMETHOD.
ENDCLASS.
******************************************************************************************************************

class ZCL_ZEXPORTTAXINV_MPC definition
  public
  inheriting from /IWBEP/CL_MGW_PUSH_ABS_MODEL
  create public .

public section.

  types:
     TS_BILLTOPARTYNODE type SDBIL_ODATA_F_PARTY_S .
  types:
TT_BILLTOPARTYNODE type standard table of TS_BILLTOPARTYNODE .
  types:
   begin of ts_text_element,
      artifact_name  type c length 40,       " technical name
      artifact_type  type c length 4,
      parent_artifact_name type c length 40, " technical name
      parent_artifact_type type c length 4,
      text_symbol    type textpoolky,
   end of ts_text_element .
  types:
         tt_text_elements type standard table of ts_text_element with key text_symbol .
  types:
     TS_BILLINGDOCUMENTITEMNODE type SDBIL_ODATA_F_BD_ITEM_STD_S .
  types:
TT_BILLINGDOCUMENTITEMNODE type standard table of TS_BILLINGDOCUMENTITEMNODE .
  types:
     TS_BILLINGDOCUMENTNODE type SDBIL_ODATA_F_BD_ROOT_STD_S .
  types:
TT_BILLINGDOCUMENTNODE type standard table of TS_BILLINGDOCUMENTNODE .
  types:
     TS_CLEAREDDOWNPAYMENTNODE type CPLDWNPAYT .
  types:
TT_CLEAREDDOWNPAYMENTNODE type standard table of TS_CLEAREDDOWNPAYMENTNODE .
  types:
     TS_CLEAREDDOWNPAYMENTOVWNODE type CPLDWNPAYT .
  types:
TT_CLEAREDDOWNPAYMENTOVWNODE type standard table of TS_CLEAREDDOWNPAYMENTOVWNODE .
  types:
     TS_COMPANYNODE type SDBIL_ODATA_F_COMPANY_S .
  types:
TT_COMPANYNODE type standard table of TS_COMPANYNODE .
  types:
     TS_DOWNPAYMENTNODE type SDBIL_ODATA_F_DOWN_PAYMENT_S .
  types:
TT_DOWNPAYMENTNODE type standard table of TS_DOWNPAYMENTNODE .
  types:
     TS_DOWNPAYMENTOVERVIEWNODE type SDBIL_ODATA_F_DP_OVERVIEW_S .
  types:
TT_DOWNPAYMENTOVERVIEWNODE type standard table of TS_DOWNPAYMENTOVERVIEWNODE .
  types:
     TS_ISRPRINTDETAILSNODE type VBDRE .
  types:
TT_ISRPRINTDETAILSNODE type standard table of TS_ISRPRINTDETAILSNODE .
  types:
     TS_INCOTERMSNODE type SDBIL_ODATA_F_INCO_TERMS_S .
  types:
TT_INCOTERMSNODE type standard table of TS_INCOTERMSNODE .
  types:
     TS_ITEMAFTERCORRNODE type SDBIL_ODATA_F_BD_ITEM_STD_S .
  types:
TT_ITEMAFTERCORRNODE type standard table of TS_ITEMAFTERCORRNODE .
  types:
     TS_ITEMBATCHDETAILSNODE type SDBIL_ODATA_F_BD_BATCH_S .
  types:
TT_ITEMBATCHDETAILSNODE type standard table of TS_ITEMBATCHDETAILSNODE .
  types:
     TS_ITEMCONFIGURATIONNODE type SDBIL_ODATA_F_ITEM_CONFIG_S .
  types:
TT_ITEMCONFIGURATIONNODE type standard table of TS_ITEMCONFIGURATIONNODE .
  types:
     TS_ITEMDIFFERENCENODE type SDBIL_ODATA_F_BD_ITEM_STD_S .
  types:
TT_ITEMDIFFERENCENODE type standard table of TS_ITEMDIFFERENCENODE .
  types:
     TS_ITEMPRICINGAFTERCORRNODE type SDBIL_ODATA_F_PRICE_COND_S .
  types:
TT_ITEMPRICINGAFTERCORRNODE type standard table of TS_ITEMPRICINGAFTERCORRNODE .
  types:
     TS_ITEMPRICINGCONDITIONNODE type SDBIL_ODATA_F_PRICE_COND_S .
  types:
TT_ITEMPRICINGCONDITIONNODE type standard table of TS_ITEMPRICINGCONDITIONNODE .
  types:
     TS_ITEMPRICINGDIFFERENCENODE type SDBIL_ODATA_F_PRICE_COND_S .
  types:
TT_ITEMPRICINGDIFFERENCENODE type standard table of TS_ITEMPRICINGDIFFERENCENODE .
  types:
     TS_ITEMSHIPTOPARTYNODE type SDBIL_ODATA_F_PARTY_S .
  types:
TT_ITEMSHIPTOPARTYNODE type standard table of TS_ITEMSHIPTOPARTYNODE .
  types:
     TS_ITEMTEXTELEMENTNODE type SDBIL_ODATA_F_TEXT_S .
  types:
TT_ITEMTEXTELEMENTNODE type standard table of TS_ITEMTEXTELEMENTNODE .
  types:
     TS_LEGALLYREQUIREDTEXTNODE type SDBIL_ODATA_F_LEGAL_TEXT_S .
  types:
TT_LEGALLYREQUIREDTEXTNODE type standard table of TS_LEGALLYREQUIREDTEXTNODE .
  types:
     TS_OPENDOWNPAYMENTNODE type CPLDWNPAYT .
  types:
TT_OPENDOWNPAYMENTNODE type standard table of TS_OPENDOWNPAYMENTNODE .
  types:
     TS_PAYERPARTYNODE type SDBIL_ODATA_F_PARTY_S .
  types:
TT_PAYERPARTYNODE type standard table of TS_PAYERPARTYNODE .
  types:
     TS_PAYMENTCARDNODE type SDBIL_ODATA_F_CREDIT_CARD_S .
  types:
TT_PAYMENTCARDNODE type standard table of TS_PAYMENTCARDNODE .
  types:
     TS_PAYMENTMETHODNODE type SDBIL_ODATA_F_PAYM_METHOD_S .
  types:
TT_PAYMENTMETHODNODE type standard table of TS_PAYMENTMETHODNODE .
  types:
     TS_PAYMENTTERMSNODE type SDBIL_ODATA_F_PAYM_TERMS_S .
  types:
TT_PAYMENTTERMSNODE type standard table of TS_PAYMENTTERMSNODE .
  types:
     TS_PRICINGCONDITIONNODE type SDBIL_ODATA_F_PRICE_COND_S .
  types:
TT_PRICINGCONDITIONNODE type standard table of TS_PRICINGCONDITIONNODE .
  types:
     TS_PRICINGTERMSNODE type SDBIL_ODATA_F_PRICING_TERMS_S .
  types:
TT_PRICINGTERMSNODE type standard table of TS_PRICINGTERMSNODE .
  types:
     TS_PROJECTDETAILSNODE type SDBIL_ODATA_F_PROJ_DETAILS_S .
  types:
TT_PROJECTDETAILSNODE type standard table of TS_PROJECTDETAILSNODE .
  types:
     TS_QUERYNODE type SDBIL_ODATA_F_BD_QUERY .
  types:
TT_QUERYNODE type standard table of TS_QUERYNODE .
  types:
     TS_SEPANODE type SDBIL_ODATA_F_SEPA_S .
  types:
TT_SEPANODE type standard table of TS_SEPANODE .
  types:
     TS_SERIALNUMBERNODE type SDBIL_ODATA_F_SERIAL_NUMBER_S .
  types:
TT_SERIALNUMBERNODE type standard table of TS_SERIALNUMBERNODE .
  types:
     TS_SHIPTOPARTYNODE type SDBIL_ODATA_F_PARTY_S .
  types:
TT_SHIPTOPARTYNODE type standard table of TS_SHIPTOPARTYNODE .
  types:
     TS_SOLDTOPARTYNODE type SDBIL_ODATA_F_PARTY_S .
  types:
TT_SOLDTOPARTYNODE type standard table of TS_SOLDTOPARTYNODE .
  types:
     TS_SUPPLIERNODE type SDBIL_ODATA_F_COMPANY_S .
  types:
TT_SUPPLIERNODE type standard table of TS_SUPPLIERNODE .
  types:
     TS_TAXATIONTERMSNODE type SDBIL_ODATA_F_TAX_TERMS_S .
  types:
TT_TAXATIONTERMSNODE type standard table of TS_TAXATIONTERMSNODE .
  types:
     TS_TEXTELEMENTNODE type SDBIL_ODATA_F_TEXT_S .
  types:
TT_TEXTELEMENTNODE type standard table of TS_TEXTELEMENTNODE .
  types:
     TS_VATSUMMARYNODE type SDBIL_ODATA_F_VAT_SUMM_S .
  types:
TT_VATSUMMARYNODE type standard table of TS_VATSUMMARYNODE .
  types:
  begin of TS_HEADER,
     BILLINGDOCUMENT type C length 10,
     INVOICE type string,
     INVOICEDATE type string,
     REFERENCE type string,
     TAXNO type string,
     CUSTOMERPONO type string,
     CUSTOMERPODATE type string,
     PAYMENTTERMS type string,
     PAYMENTTERMDESCRIPTION type string,
     INCOTERMS type string,
     BILLFROMPLANT type string,
     BILLFROMADDRESS type string,
     BILLFROMGST type string,
     BILLFROMPAN type string,
     BILLFROMIEC type string,
     BILLFROMIECDT type string,
     BILLFROMSTATECODE type string,
     BILLFROMSUPPCODE type string,
     BILLFROMCIN type string,
     BILLTOCUSTOMERCODE type string,
     BILLTOADDRESS type string,
     BILLTOGST type string,
     BILLTOPAN type string,
     BILLTOIEC type string,
     BILLTOSTATECODE type string,
     BILLTOCIN type string,
     SHIPFROMPLANT type string,
     SHIPFROMADDRESS type string,
     SHIPFROMGST type string,
     SHIPFROMPAN type string,
     SHIPFROMIEC type string,
     SHIPFROMIECDT type string,
     SHIPFROMSTATECODE type string,
     SHIPFROMCIN type string,
     SHIPTOCUSTOMERCODE type string,
     SHIPTOADDRESS type string,
     SHIPTOGST type string,
     SHIPTOPAN type string,
     SHIPTOIEC type string,
     SHIPTOSTATECODE type string,
     SHIPTOCIN type string,
     VENDORCODE type string,
     TRANSPORTERNAME type string,
     TRANSPORTERGSTIN type string,
     MODEOFDELIVERY type string,
     VEHICLETYPE type string,
     VEHICLENO type string,
     DISTANCE type string,
     LRDOCKETNO type string,
     LRDOCKETDATE type string,
     REMARKS type string,
     IRN type string,
     EWAYBILLNO type string,
     EWAYBILLDATE type string,
     TAXABLEVALUE type string,
     CUSTOMERJOB type string,
     LUTDATE type string,
     LUTNO type string,
     FINANCIALYEAR type string,
     COMMERCIALINVNO type string,
     COMMERCIALDATE type string,
     EINV type string,
     TYPEOFEXPORT type string,
     LICENCENUMBER type string,
  end of TS_HEADER .
  types:
TT_HEADER type standard table of TS_HEADER .
  types:
  begin of TS_ITEMDATA,
     BILLINGDOCUMENT type string,
     MATERIALCODE type string,
     MATERIALCODEDESCRPTION type string,
     CUSTOMERMATERIALCODE type string,
     CUSTOMERMATERIALDESCRIPTION type string,
     HSNSAC type string,
     UOM type string,
     QUNTITY type string,
     UNITPRISE type string,
     DISCOUNT type string,
     DISCVALUE type string,
     VALUEAFTERDISCOUNT type string,
     TATOLBASICVALUE type string,
     TOTALDISCOUNT type string,
     VALUE type string,
     FREIGHTCHARGES type string,
     PACKAGINGCHARGES type string,
     TOOLAMORTIZATIONCHARGES type string,
     TAXABLEVALUE type string,
     IGST type string,
     IGSTVALUE type string,
     CGST type string,
     CGSTVALUE type string,
     SGSTVALUE type string,
     SGST type string,
     TCSVALUE type string,
     TCS type string,
     TOTALINVOICEVALUE type string,
     IGSTTOT type string,
     IGSTVALUETOT type string,
     CGSTTOT type string,
     CGSTVALUETOT type string,
     SGSTVALUETOT type string,
     SGSTTOT type string,
     TCSVALUETOT type string,
     TCSTOT type string,
     EMPTYVALUE type string,
     GSTAMTWORDS type string,
     INVAMTWORDS type string,
     VALUE2 type string,
     TOTALBASIC type string,
     EINVOICEQRC type string,
     LESSTAXABLEVALUE type string,
     CUSTOMERQRC type string,
     EMPTYVALUEQRC type string,
     HSNDESCRIPTION type string,
     QRCCUSTOMER type string,
  end of TS_ITEMDATA .
  types:
TT_ITEMDATA type standard table of TS_ITEMDATA .
  types:
  begin of TS_FOOTER,
     BILLINGDOCUMENT type C length 10,
     NAME type string,
     VALUE type string,
     NAMESIGN type string,
     NAMESIGNVAL type string,
  end of TS_FOOTER .
  types:
TT_FOOTER type standard table of TS_FOOTER .

  constants GC_VATSUMMARYNODE type /IWBEP/IF_MGW_MED_ODATA_TYPES=>TY_E_MED_ENTITY_NAME value 'VATSummaryNode' ##NO_TEXT.
  constants GC_TEXTELEMENTNODE type /IWBEP/IF_MGW_MED_ODATA_TYPES=>TY_E_MED_ENTITY_NAME value 'TextElementNode' ##NO_TEXT.
  constants GC_TAXATIONTERMSNODE type /IWBEP/IF_MGW_MED_ODATA_TYPES=>TY_E_MED_ENTITY_NAME value 'TaxationTermsNode' ##NO_TEXT.
  constants GC_SUPPLIERNODE type /IWBEP/IF_MGW_MED_ODATA_TYPES=>TY_E_MED_ENTITY_NAME value 'SupplierNode' ##NO_TEXT.
  constants GC_SOLDTOPARTYNODE type /IWBEP/IF_MGW_MED_ODATA_TYPES=>TY_E_MED_ENTITY_NAME value 'SoldToPartyNode' ##NO_TEXT.
  constants GC_SHIPTOPARTYNODE type /IWBEP/IF_MGW_MED_ODATA_TYPES=>TY_E_MED_ENTITY_NAME value 'ShipToPartyNode' ##NO_TEXT.
  constants GC_SERIALNUMBERNODE type /IWBEP/IF_MGW_MED_ODATA_TYPES=>TY_E_MED_ENTITY_NAME value 'SerialNumberNode' ##NO_TEXT.
  constants GC_SEPANODE type /IWBEP/IF_MGW_MED_ODATA_TYPES=>TY_E_MED_ENTITY_NAME value 'SEPANode' ##NO_TEXT.
  constants GC_QUERYNODE type /IWBEP/IF_MGW_MED_ODATA_TYPES=>TY_E_MED_ENTITY_NAME value 'QueryNode' ##NO_TEXT.
  constants GC_PROJECTDETAILSNODE type /IWBEP/IF_MGW_MED_ODATA_TYPES=>TY_E_MED_ENTITY_NAME value 'ProjectDetailsNode' ##NO_TEXT.
  constants GC_PRICINGTERMSNODE type /IWBEP/IF_MGW_MED_ODATA_TYPES=>TY_E_MED_ENTITY_NAME value 'PricingTermsNode' ##NO_TEXT.
  constants GC_PRICINGCONDITIONNODE type /IWBEP/IF_MGW_MED_ODATA_TYPES=>TY_E_MED_ENTITY_NAME value 'PricingConditionNode' ##NO_TEXT.
  constants GC_PAYMENTTERMSNODE type /IWBEP/IF_MGW_MED_ODATA_TYPES=>TY_E_MED_ENTITY_NAME value 'PaymentTermsNode' ##NO_TEXT.
  constants GC_PAYMENTMETHODNODE type /IWBEP/IF_MGW_MED_ODATA_TYPES=>TY_E_MED_ENTITY_NAME value 'PaymentMethodNode' ##NO_TEXT.
  constants GC_PAYMENTCARDNODE type /IWBEP/IF_MGW_MED_ODATA_TYPES=>TY_E_MED_ENTITY_NAME value 'PaymentCardNode' ##NO_TEXT.
  constants GC_PAYERPARTYNODE type /IWBEP/IF_MGW_MED_ODATA_TYPES=>TY_E_MED_ENTITY_NAME value 'PayerPartyNode' ##NO_TEXT.
  constants GC_OPENDOWNPAYMENTNODE type /IWBEP/IF_MGW_MED_ODATA_TYPES=>TY_E_MED_ENTITY_NAME value 'OpenDownPaymentNode' ##NO_TEXT.
  constants GC_LEGALLYREQUIREDTEXTNODE type /IWBEP/IF_MGW_MED_ODATA_TYPES=>TY_E_MED_ENTITY_NAME value 'LegallyRequiredTextNode' ##NO_TEXT.
  constants GC_ITEMTEXTELEMENTNODE type /IWBEP/IF_MGW_MED_ODATA_TYPES=>TY_E_MED_ENTITY_NAME value 'ItemTextElementNode' ##NO_TEXT.
  constants GC_ITEMSHIPTOPARTYNODE type /IWBEP/IF_MGW_MED_ODATA_TYPES=>TY_E_MED_ENTITY_NAME value 'ItemShipToPartyNode' ##NO_TEXT.
  constants GC_ITEMPRICINGDIFFERENCENODE type /IWBEP/IF_MGW_MED_ODATA_TYPES=>TY_E_MED_ENTITY_NAME value 'ItemPricingDifferenceNode' ##NO_TEXT.
  constants GC_ITEMPRICINGCONDITIONNODE type /IWBEP/IF_MGW_MED_ODATA_TYPES=>TY_E_MED_ENTITY_NAME value 'ItemPricingConditionNode' ##NO_TEXT.
  constants GC_ITEMPRICINGAFTERCORRNODE type /IWBEP/IF_MGW_MED_ODATA_TYPES=>TY_E_MED_ENTITY_NAME value 'ItemPricingAfterCorrNode' ##NO_TEXT.
  constants GC_ITEMDIFFERENCENODE type /IWBEP/IF_MGW_MED_ODATA_TYPES=>TY_E_MED_ENTITY_NAME value 'ItemDifferenceNode' ##NO_TEXT.
  constants GC_ITEMDATA type /IWBEP/IF_MGW_MED_ODATA_TYPES=>TY_E_MED_ENTITY_NAME value 'ItemData' ##NO_TEXT.
  constants GC_ITEMCONFIGURATIONNODE type /IWBEP/IF_MGW_MED_ODATA_TYPES=>TY_E_MED_ENTITY_NAME value 'ItemConfigurationNode' ##NO_TEXT.
  constants GC_ITEMBATCHDETAILSNODE type /IWBEP/IF_MGW_MED_ODATA_TYPES=>TY_E_MED_ENTITY_NAME value 'ItemBatchDetailsNode' ##NO_TEXT.
  constants GC_ITEMAFTERCORRNODE type /IWBEP/IF_MGW_MED_ODATA_TYPES=>TY_E_MED_ENTITY_NAME value 'ItemAfterCorrNode' ##NO_TEXT.
  constants GC_ISRPRINTDETAILSNODE type /IWBEP/IF_MGW_MED_ODATA_TYPES=>TY_E_MED_ENTITY_NAME value 'ISRPrintDetailsNode' ##NO_TEXT.
  constants GC_INCOTERMSNODE type /IWBEP/IF_MGW_MED_ODATA_TYPES=>TY_E_MED_ENTITY_NAME value 'IncotermsNode' ##NO_TEXT.
  constants GC_HEADER type /IWBEP/IF_MGW_MED_ODATA_TYPES=>TY_E_MED_ENTITY_NAME value 'Header' ##NO_TEXT.
  constants GC_FOOTER type /IWBEP/IF_MGW_MED_ODATA_TYPES=>TY_E_MED_ENTITY_NAME value 'Footer' ##NO_TEXT.
  constants GC_DOWNPAYMENTOVERVIEWNODE type /IWBEP/IF_MGW_MED_ODATA_TYPES=>TY_E_MED_ENTITY_NAME value 'DownPaymentOverviewNode' ##NO_TEXT.
  constants GC_DOWNPAYMENTNODE type /IWBEP/IF_MGW_MED_ODATA_TYPES=>TY_E_MED_ENTITY_NAME value 'DownPaymentNode' ##NO_TEXT.
  constants GC_COMPANYNODE type /IWBEP/IF_MGW_MED_ODATA_TYPES=>TY_E_MED_ENTITY_NAME value 'CompanyNode' ##NO_TEXT.
  constants GC_CLEAREDDOWNPAYMENTOVWNODE type /IWBEP/IF_MGW_MED_ODATA_TYPES=>TY_E_MED_ENTITY_NAME value 'ClearedDownPaymentOvwNode' ##NO_TEXT.
  constants GC_CLEAREDDOWNPAYMENTNODE type /IWBEP/IF_MGW_MED_ODATA_TYPES=>TY_E_MED_ENTITY_NAME value 'ClearedDownPaymentNode' ##NO_TEXT.
  constants GC_BILLTOPARTYNODE type /IWBEP/IF_MGW_MED_ODATA_TYPES=>TY_E_MED_ENTITY_NAME value 'BillToPartyNode' ##NO_TEXT.
  constants GC_BILLINGDOCUMENTNODE type /IWBEP/IF_MGW_MED_ODATA_TYPES=>TY_E_MED_ENTITY_NAME value 'BillingDocumentNode' ##NO_TEXT.
  constants GC_BILLINGDOCUMENTITEMNODE type /IWBEP/IF_MGW_MED_ODATA_TYPES=>TY_E_MED_ENTITY_NAME value 'BillingDocumentItemNode' ##NO_TEXT.

  methods GET_EXTENDED_MODEL
  final
    exporting
      !EV_EXTENDED_SERVICE type /IWBEP/MED_GRP_TECHNICAL_NAME
      !EV_EXT_SERVICE_VERSION type /IWBEP/MED_GRP_VERSION
      !EV_EXTENDED_MODEL type /IWBEP/MED_MDL_TECHNICAL_NAME
      !EV_EXT_MODEL_VERSION type /IWBEP/MED_MDL_VERSION
    raising
      /IWBEP/CX_MGW_MED_EXCEPTION .
  methods LOAD_TEXT_ELEMENTS
  final
    returning
      value(RT_TEXT_ELEMENTS) type TT_TEXT_ELEMENTS
    raising
      /IWBEP/CX_MGW_MED_EXCEPTION .

  methods DEFINE
    redefinition .
  methods GET_LAST_MODIFIED
    redefinition .
protected section.
private section.

  constants GC_INCL_NAME type STRING value 'ZCL_ZEXPORTTAXINV_MPC=========CP' ##NO_TEXT.

  methods CHANGE_LABELS
    raising
      /IWBEP/CX_MGW_MED_EXCEPTION .
  methods CREATE_NEW_ARTIFACTS
    raising
      /IWBEP/CX_MGW_MED_EXCEPTION .
ENDCLASS.



CLASS ZCL_ZEXPORTTAXINV_MPC IMPLEMENTATION.


  method CHANGE_LABELS.
*&---------------------------------------------------------------------*
*&           Generated code for the MODEL PROVIDER BASE CLASS          &*
*&                                                                     &*
*&  !!!NEVER MODIFY THIS CLASS. IN CASE YOU WANT TO CHANGE THE MODEL   &*
*&        DO THIS IN THE MODEL PROVIDER SUBCLASS!!!                    &*
*&                                                                     &*
*&---------------------------------------------------------------------*


data:
  lo_entity_type    type ref to /iwbep/if_mgw_odata_entity_typ,           "#EC NEEDED
  lo_complex_type   type ref to /iwbep/if_mgw_odata_cmplx_type,           "#EC NEEDED
  lo_property       type ref to /iwbep/if_mgw_odata_property,             "#EC NEEDED
  lo_association    type ref to /iwbep/if_mgw_odata_assoc,                "#EC NEEDED
  lo_assoc_set      type ref to /iwbep/if_mgw_odata_assoc_set,            "#EC NEEDED
  lo_ref_constraint type ref to /iwbep/if_mgw_odata_ref_constr,           "#EC NEEDED
  lo_nav_property   type ref to /iwbep/if_mgw_odata_nav_prop,             "#EC NEEDED
  lo_action         type ref to /iwbep/if_mgw_odata_action,               "#EC NEEDED
  lo_parameter      type ref to /iwbep/if_mgw_odata_property,             "#EC NEEDED
  lo_entity_set     type ref to /iwbep/if_mgw_odata_entity_set.           "#EC NEEDED


* Change the labels for the entity types' properties
   lo_entity_type = model->get_entity_type( iv_entity_name = 'BillToPartyNode' )."#EC NOTEXT
lo_property = lo_entity_type->get_property( iv_property_name = 'BillingDocument' )."#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '001' iv_text_element_container = gc_incl_name )."#EC NOTEXT
   lo_entity_type = model->get_entity_type( iv_entity_name = 'IncotermsNode' )."#EC NOTEXT
lo_property = lo_entity_type->get_property( iv_property_name = 'BillingDocument' )."#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '002' iv_text_element_container = gc_incl_name )."#EC NOTEXT
   lo_entity_type = model->get_entity_type( iv_entity_name = 'ItemPricingConditionNode' )."#EC NOTEXT
lo_property = lo_entity_type->get_property( iv_property_name = 'BillingDocument' )."#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '003' iv_text_element_container = gc_incl_name )."#EC NOTEXT
   lo_entity_type = model->get_entity_type( iv_entity_name = 'ItemPricingConditionNode' )."#EC NOTEXT
lo_property = lo_entity_type->get_property( iv_property_name = 'BillingDocumentItem' )."#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '004' iv_text_element_container = gc_incl_name )."#EC NOTEXT
   lo_entity_type = model->get_entity_type( iv_entity_name = 'ItemShipToPartyNode' )."#EC NOTEXT
lo_property = lo_entity_type->get_property( iv_property_name = 'BillingDocument' )."#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '005' iv_text_element_container = gc_incl_name )."#EC NOTEXT
   lo_entity_type = model->get_entity_type( iv_entity_name = 'ItemShipToPartyNode' )."#EC NOTEXT
lo_property = lo_entity_type->get_property( iv_property_name = 'BillingDocumentItem' )."#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '006' iv_text_element_container = gc_incl_name )."#EC NOTEXT
   lo_entity_type = model->get_entity_type( iv_entity_name = 'ItemTextElementNode' )."#EC NOTEXT
lo_property = lo_entity_type->get_property( iv_property_name = 'BillingDocument' )."#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '007' iv_text_element_container = gc_incl_name )."#EC NOTEXT
   lo_entity_type = model->get_entity_type( iv_entity_name = 'ItemTextElementNode' )."#EC NOTEXT
lo_property = lo_entity_type->get_property( iv_property_name = 'BillingDocumentItem' )."#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '008' iv_text_element_container = gc_incl_name )."#EC NOTEXT
   lo_entity_type = model->get_entity_type( iv_entity_name = 'LegallyRequiredTextNode' )."#EC NOTEXT
lo_property = lo_entity_type->get_property( iv_property_name = 'BillingDocument' )."#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '009' iv_text_element_container = gc_incl_name )."#EC NOTEXT
   lo_entity_type = model->get_entity_type( iv_entity_name = 'PayerPartyNode' )."#EC NOTEXT
lo_property = lo_entity_type->get_property( iv_property_name = 'BillingDocument' )."#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '010' iv_text_element_container = gc_incl_name )."#EC NOTEXT
   lo_entity_type = model->get_entity_type( iv_entity_name = 'PaymentMethodNode' )."#EC NOTEXT
lo_property = lo_entity_type->get_property( iv_property_name = 'BillingDocument' )."#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '011' iv_text_element_container = gc_incl_name )."#EC NOTEXT
   lo_entity_type = model->get_entity_type( iv_entity_name = 'PaymentTermsNode' )."#EC NOTEXT
lo_property = lo_entity_type->get_property( iv_property_name = 'BillingDocument' )."#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '012' iv_text_element_container = gc_incl_name )."#EC NOTEXT
   lo_entity_type = model->get_entity_type( iv_entity_name = 'PricingConditionNode' )."#EC NOTEXT
lo_property = lo_entity_type->get_property( iv_property_name = 'BillingDocument' )."#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '013' iv_text_element_container = gc_incl_name )."#EC NOTEXT
   lo_entity_type = model->get_entity_type( iv_entity_name = 'PricingTermsNode' )."#EC NOTEXT
lo_property = lo_entity_type->get_property( iv_property_name = 'BillingDocument' )."#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '014' iv_text_element_container = gc_incl_name )."#EC NOTEXT
   lo_entity_type = model->get_entity_type( iv_entity_name = 'ShipToPartyNode' )."#EC NOTEXT
lo_property = lo_entity_type->get_property( iv_property_name = 'BillingDocument' )."#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '015' iv_text_element_container = gc_incl_name )."#EC NOTEXT
   lo_entity_type = model->get_entity_type( iv_entity_name = 'SoldToPartyNode' )."#EC NOTEXT
lo_property = lo_entity_type->get_property( iv_property_name = 'BillingDocument' )."#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '016' iv_text_element_container = gc_incl_name )."#EC NOTEXT
   lo_entity_type = model->get_entity_type( iv_entity_name = 'TaxationTermsNode' )."#EC NOTEXT
lo_property = lo_entity_type->get_property( iv_property_name = 'BillingDocument' )."#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '017' iv_text_element_container = gc_incl_name )."#EC NOTEXT
   lo_entity_type = model->get_entity_type( iv_entity_name = 'TextElementNode' )."#EC NOTEXT
lo_property = lo_entity_type->get_property( iv_property_name = 'BillingDocument' )."#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '018' iv_text_element_container = gc_incl_name )."#EC NOTEXT
   lo_entity_type = model->get_entity_type( iv_entity_name = 'VATSummaryNode' )."#EC NOTEXT
lo_property = lo_entity_type->get_property( iv_property_name = 'BillingDocument' )."#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '019' iv_text_element_container = gc_incl_name )."#EC NOTEXT
  endmethod.


  method CREATE_NEW_ARTIFACTS.
*&---------------------------------------------------------------------*
*&           Generated code for the MODEL PROVIDER BASE CLASS          &*
*&                                                                     &*
*&  !!!NEVER MODIFY THIS CLASS. IN CASE YOU WANT TO CHANGE THE MODEL   &*
*&        DO THIS IN THE MODEL PROVIDER SUBCLASS!!!                    &*
*&                                                                     &*
*&---------------------------------------------------------------------*


DATA:
  lo_entity_type    TYPE REF TO /iwbep/if_mgw_odata_entity_typ,                      "#EC NEEDED
  lo_complex_type   TYPE REF TO /iwbep/if_mgw_odata_cmplx_type,                      "#EC NEEDED
  lo_property       TYPE REF TO /iwbep/if_mgw_odata_property,                        "#EC NEEDED
  lo_association    TYPE REF TO /iwbep/if_mgw_odata_assoc,                           "#EC NEEDED
  lo_assoc_set      TYPE REF TO /iwbep/if_mgw_odata_assoc_set,                       "#EC NEEDED
  lo_ref_constraint TYPE REF TO /iwbep/if_mgw_odata_ref_constr,                      "#EC NEEDED
  lo_nav_property   TYPE REF TO /iwbep/if_mgw_odata_nav_prop,                        "#EC NEEDED
  lo_action         TYPE REF TO /iwbep/if_mgw_odata_action,                          "#EC NEEDED
  lo_parameter      TYPE REF TO /iwbep/if_mgw_odata_property,                        "#EC NEEDED
  lo_entity_set     TYPE REF TO /iwbep/if_mgw_odata_entity_set.                      "#EC NEEDED


***********************************************************************************************************************************
*   ENTITY - Header
***********************************************************************************************************************************
lo_entity_type = model->create_entity_type( iv_entity_type_name = 'Header' iv_def_entity_set = abap_false ). "#EC NOTEXT

***********************************************************************************************************************************
*Properties
***********************************************************************************************************************************

lo_property = lo_entity_type->create_property( iv_property_name = 'BillingDocument' iv_abap_fieldname = 'BILLINGDOCUMENT' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '020' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_is_key( ).
lo_property->set_type_edm_string( ).
lo_property->set_maxlength( iv_max_length = 10 ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'Invoice' iv_abap_fieldname = 'INVOICE' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '021' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'InvoiceDate' iv_abap_fieldname = 'INVOICEDATE' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '022' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'Reference' iv_abap_fieldname = 'REFERENCE' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '023' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'Taxno' iv_abap_fieldname = 'TAXNO' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '024' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'CustomerPoNo' iv_abap_fieldname = 'CUSTOMERPONO' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '025' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'CustomerPoDate' iv_abap_fieldname = 'CUSTOMERPODATE' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '026' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'PaymentTerms' iv_abap_fieldname = 'PAYMENTTERMS' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '027' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'PaymentTermsDescription' iv_abap_fieldname = 'PAYMENTTERMDESCRIPTION' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '028' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'IncoTerms' iv_abap_fieldname = 'INCOTERMS' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '029' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'BillFromPlant' iv_abap_fieldname = 'BILLFROMPLANT' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '030' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'BillFromAddress' iv_abap_fieldname = 'BILLFROMADDRESS' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '031' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'BillFromGST' iv_abap_fieldname = 'BILLFROMGST' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '032' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'BillFromPan' iv_abap_fieldname = 'BILLFROMPAN' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '033' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'BillFromIec' iv_abap_fieldname = 'BILLFROMIEC' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '034' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'BillFromIecDt' iv_abap_fieldname = 'BILLFROMIECDT' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '131' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'BillFromStatecode' iv_abap_fieldname = 'BILLFROMSTATECODE' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '035' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'BillFromSuppCode' iv_abap_fieldname = 'BILLFROMSUPPCODE' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '036' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'BillFromCin' iv_abap_fieldname = 'BILLFROMCIN' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '037' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'BillToCustomerCode' iv_abap_fieldname = 'BILLTOCUSTOMERCODE' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '038' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'BillToAddress' iv_abap_fieldname = 'BILLTOADDRESS' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '039' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'BillToGST' iv_abap_fieldname = 'BILLTOGST' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '040' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'BillToPan' iv_abap_fieldname = 'BILLTOPAN' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '041' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'BillToIec' iv_abap_fieldname = 'BILLTOIEC' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '042' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'BillToStatecode' iv_abap_fieldname = 'BILLTOSTATECODE' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '043' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'BillToCin' iv_abap_fieldname = 'BILLTOCIN' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '044' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'ShipfromPlant' iv_abap_fieldname = 'SHIPFROMPLANT' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '045' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'ShipfromAddress' iv_abap_fieldname = 'SHIPFROMADDRESS' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '046' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'ShipfromGST' iv_abap_fieldname = 'SHIPFROMGST' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '047' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'ShipfromPan' iv_abap_fieldname = 'SHIPFROMPAN' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '048' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'ShipfromIec' iv_abap_fieldname = 'SHIPFROMIEC' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '049' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'ShipfromIecDt' iv_abap_fieldname = 'SHIPFROMIECDT' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '132' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'ShipfromStatecode' iv_abap_fieldname = 'SHIPFROMSTATECODE' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '050' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'ShipfromCin' iv_abap_fieldname = 'SHIPFROMCIN' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '051' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'ShipToCustomeCode' iv_abap_fieldname = 'SHIPTOCUSTOMERCODE' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '052' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'ShipToAddress' iv_abap_fieldname = 'SHIPTOADDRESS' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '053' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'ShipToGST' iv_abap_fieldname = 'SHIPTOGST' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '054' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'ShipToPan' iv_abap_fieldname = 'SHIPTOPAN' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '055' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'ShipToIec' iv_abap_fieldname = 'SHIPTOIEC' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '056' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'ShipToStatecode' iv_abap_fieldname = 'SHIPTOSTATECODE' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '057' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'ShipToCin' iv_abap_fieldname = 'SHIPTOCIN' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '058' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'VendorCode' iv_abap_fieldname = 'VENDORCODE' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '059' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'TransporterName' iv_abap_fieldname = 'TRANSPORTERNAME' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '060' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'TransporterGstin' iv_abap_fieldname = 'TRANSPORTERGSTIN' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '061' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'ModeofDelivery' iv_abap_fieldname = 'MODEOFDELIVERY' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '062' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'Vehicletype' iv_abap_fieldname = 'VEHICLETYPE' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '063' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'VehicleNo' iv_abap_fieldname = 'VEHICLENO' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '064' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'Distance' iv_abap_fieldname = 'DISTANCE' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '065' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'LrdocketNo' iv_abap_fieldname = 'LRDOCKETNO' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '066' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'LrdocketDate' iv_abap_fieldname = 'LRDOCKETDATE' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '067' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'Remarks' iv_abap_fieldname = 'REMARKS' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '068' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'IRN' iv_abap_fieldname = 'IRN' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '069' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'EwayBillNo' iv_abap_fieldname = 'EWAYBILLNO' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '070' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'EwayBillDate' iv_abap_fieldname = 'EWAYBILLDATE' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '071' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'TaxableValue' iv_abap_fieldname = 'TAXABLEVALUE' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '072' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'CustomerJob' iv_abap_fieldname = 'CUSTOMERJOB' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '073' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'LutDate' iv_abap_fieldname = 'LUTDATE' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '126' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'LutNo' iv_abap_fieldname = 'LUTNO' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '127' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'Financialyear' iv_abap_fieldname = 'FINANCIALYEAR' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '128' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'CommercialInvNo' iv_abap_fieldname = 'COMMERCIALINVNO' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '129' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'CommercialDate' iv_abap_fieldname = 'COMMERCIALDATE' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '130' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'Einv' iv_abap_fieldname = 'EINV' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '133' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'TypeofExport' iv_abap_fieldname = 'TYPEOFEXPORT' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '134' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'LicenceNumber' iv_abap_fieldname = 'LICENCENUMBER' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '135' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).

lo_entity_type->bind_structure( iv_structure_name  = 'ZCL_ZEXPORTTAXINV_MPC=>TS_HEADER' ). "#EC NOTEXT


lo_entity_type = model->create_entity_type( iv_entity_type_name = 'ItemData' iv_def_entity_set = abap_false ). "#EC NOTEXT

***********************************************************************************************************************************
*Properties
***********************************************************************************************************************************

lo_property = lo_entity_type->create_property( iv_property_name = 'BillingDocument' iv_abap_fieldname = 'BILLINGDOCUMENT' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '074' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_is_key( ).
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'MaterialCode' iv_abap_fieldname = 'MATERIALCODE' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '075' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'MaterialCodeDescription' iv_abap_fieldname = 'MATERIALCODEDESCRPTION' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '076' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'CustomerMaterialCode' iv_abap_fieldname = 'CUSTOMERMATERIALCODE' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '077' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'CustomerMaterialDescription' iv_abap_fieldname = 'CUSTOMERMATERIALDESCRIPTION' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '078' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'HsnSac' iv_abap_fieldname = 'HSNSAC' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '079' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'Uom' iv_abap_fieldname = 'UOM' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '080' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'Quntity' iv_abap_fieldname = 'QUNTITY' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '081' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'UnitPrise' iv_abap_fieldname = 'UNITPRISE' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '082' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'Discount' iv_abap_fieldname = 'DISCOUNT' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '083' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'DiscValue' iv_abap_fieldname = 'DISCVALUE' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '084' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'ValueafterDiscount' iv_abap_fieldname = 'VALUEAFTERDISCOUNT' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '085' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'TotalBasicValue' iv_abap_fieldname = 'TATOLBASICVALUE' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '086' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'TotalDiscount' iv_abap_fieldname = 'TOTALDISCOUNT' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '087' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'Value' iv_abap_fieldname = 'VALUE' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '088' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'FreightCharges' iv_abap_fieldname = 'FREIGHTCHARGES' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '089' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'PackagingCharges' iv_abap_fieldname = 'PACKAGINGCHARGES' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '090' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'ToolAmortizationCharges' iv_abap_fieldname = 'TOOLAMORTIZATIONCHARGES' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '091' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'TaxableValue' iv_abap_fieldname = 'TAXABLEVALUE' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '092' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'Igst' iv_abap_fieldname = 'IGST' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '093' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'IgstValue' iv_abap_fieldname = 'IGSTVALUE' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '094' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'Cgst' iv_abap_fieldname = 'CGST' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '095' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'CgstValue' iv_abap_fieldname = 'CGSTVALUE' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '096' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'SgstValue' iv_abap_fieldname = 'SGSTVALUE' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '097' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'Sgst' iv_abap_fieldname = 'SGST' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '098' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'TcsValue' iv_abap_fieldname = 'TCSVALUE' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '099' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'Tcs' iv_abap_fieldname = 'TCS' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '100' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'TotalInvoiceValue' iv_abap_fieldname = 'TOTALINVOICEVALUE' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '101' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'IgstTot' iv_abap_fieldname = 'IGSTTOT' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '102' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'IgstValueTot' iv_abap_fieldname = 'IGSTVALUETOT' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '103' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'CgstTot' iv_abap_fieldname = 'CGSTTOT' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '104' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'CgstValueTot' iv_abap_fieldname = 'CGSTVALUETOT' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '105' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'SgstValueTot' iv_abap_fieldname = 'SGSTVALUETOT' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '106' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'SgstTot' iv_abap_fieldname = 'SGSTTOT' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '107' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'TcsValueTot' iv_abap_fieldname = 'TCSVALUETOT' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '108' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'TcsTot' iv_abap_fieldname = 'TCSTOT' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '109' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'EmptyValue' iv_abap_fieldname = 'EMPTYVALUE' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '110' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'GSTamtwords' iv_abap_fieldname = 'GSTAMTWORDS' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '111' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'Invamtwords' iv_abap_fieldname = 'INVAMTWORDS' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '112' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'Value2' iv_abap_fieldname = 'VALUE2' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '113' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'TotalBasic' iv_abap_fieldname = 'TOTALBASIC' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '114' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'EInvoiceQRC' iv_abap_fieldname = 'EINVOICEQRC' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '115' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'LessTaxablevalue' iv_abap_fieldname = 'LESSTAXABLEVALUE' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '116' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'CustomerQRC' iv_abap_fieldname = 'CUSTOMERQRC' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '117' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'EmptyValueQRC' iv_abap_fieldname = 'EMPTYVALUEQRC' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '118' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'HSNDescription' iv_abap_fieldname = 'HSNDESCRIPTION' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '119' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'QRCCustomer' iv_abap_fieldname = 'QRCCUSTOMER' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '120' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).

lo_entity_type->bind_structure( iv_structure_name  = 'ZCL_ZEXPORTTAXINV_MPC=>TS_ITEMDATA' ). "#EC NOTEXT


lo_entity_type = model->create_entity_type( iv_entity_type_name = 'Footer' iv_def_entity_set = abap_false ). "#EC NOTEXT

***********************************************************************************************************************************
*Properties
***********************************************************************************************************************************

lo_property = lo_entity_type->create_property( iv_property_name = 'BillingDocument' iv_abap_fieldname = 'BILLINGDOCUMENT' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '121' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_is_key( ).
lo_property->set_type_edm_string( ).
lo_property->set_maxlength( iv_max_length = 10 ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'Name' iv_abap_fieldname = 'NAME' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '122' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'Value' iv_abap_fieldname = 'VALUE' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '123' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'NameSign' iv_abap_fieldname = 'NAMESIGN' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '124' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).
lo_property = lo_entity_type->create_property( iv_property_name = 'NameSignVal' iv_abap_fieldname = 'NAMESIGNVAL' ). "#EC NOTEXT
lo_property->set_label_from_text_element( iv_text_element_symbol = '125' iv_text_element_container = gc_incl_name ). "#EC NOTEXT
lo_property->set_type_edm_string( ).
lo_property->set_creatable( abap_false ).
lo_property->set_updatable( abap_false ).
lo_property->set_sortable( abap_false ).
lo_property->set_nullable( abap_false ).
lo_property->set_filterable( abap_false ).

lo_entity_type->bind_structure( iv_structure_name  = 'ZCL_ZEXPORTTAXINV_MPC=>TS_FOOTER' ). "#EC NOTEXT


***********************************************************************************************************************************
*   ENTITY SETS
***********************************************************************************************************************************
lo_entity_type = model->get_entity_type( iv_entity_name = 'Header' ). "#EC NOTEXT
lo_entity_set = lo_entity_type->create_entity_set( 'HeaderSet' ). "#EC NOTEXT

lo_entity_set->set_creatable( abap_false ).
lo_entity_set->set_updatable( abap_false ).
lo_entity_set->set_deletable( abap_false ).

lo_entity_set->set_pageable( abap_false ).
lo_entity_set->set_addressable( abap_false ).
lo_entity_set->set_has_ftxt_search( abap_false ).
lo_entity_set->set_subscribable( abap_false ).
lo_entity_set->set_filter_required( abap_false ).
lo_entity_type = model->get_entity_type( iv_entity_name = 'ItemData' ). "#EC NOTEXT
lo_entity_set = lo_entity_type->create_entity_set( 'ItemDataSet' ). "#EC NOTEXT

lo_entity_set->set_creatable( abap_false ).
lo_entity_set->set_updatable( abap_false ).
lo_entity_set->set_deletable( abap_false ).

lo_entity_set->set_pageable( abap_false ).
lo_entity_set->set_addressable( abap_false ).
lo_entity_set->set_has_ftxt_search( abap_false ).
lo_entity_set->set_subscribable( abap_false ).
lo_entity_set->set_filter_required( abap_false ).
lo_entity_type = model->get_entity_type( iv_entity_name = 'Footer' ). "#EC NOTEXT
lo_entity_set = lo_entity_type->create_entity_set( 'FooterSet' ). "#EC NOTEXT

lo_entity_set->set_creatable( abap_false ).
lo_entity_set->set_updatable( abap_false ).
lo_entity_set->set_deletable( abap_false ).

lo_entity_set->set_pageable( abap_false ).
lo_entity_set->set_addressable( abap_false ).
lo_entity_set->set_has_ftxt_search( abap_false ).
lo_entity_set->set_subscribable( abap_false ).
lo_entity_set->set_filter_required( abap_false ).


***********************************************************************************************************************************
*   new_associations
***********************************************************************************************************************************

 lo_association = model->create_association(
                            iv_association_name = 'HeaderData' "#EC NOTEXT
                            iv_left_type        = 'BillingDocumentNode' "#EC NOTEXT
                            iv_right_type       = 'Header' "#EC NOTEXT
                            iv_right_card       = '1' "#EC NOTEXT
                            iv_left_card        = '1' ). "#EC NOTEXT
* Referential constraint for association - HeaderData
lo_ref_constraint = lo_association->create_ref_constraint( ).
lo_ref_constraint->add_property( iv_principal_property = 'BillingDocument'   iv_dependent_property = 'BillingDocument' )."#EC NOTEXT
* Association Sets for association - HeaderData
lo_assoc_set = lo_association->create_assoc_set( iv_assoc_set_name = 'HeaderDataSet' ). "#EC NOTEXT
 lo_association = model->create_association(
                            iv_association_name = 'FooterData' "#EC NOTEXT
                            iv_left_type        = 'BillingDocumentNode' "#EC NOTEXT
                            iv_right_type       = 'Footer' "#EC NOTEXT
                            iv_right_card       = 'N' "#EC NOTEXT
                            iv_left_card        = '1' ). "#EC NOTEXT
* Referential constraint for association - FooterData
lo_ref_constraint = lo_association->create_ref_constraint( ).
lo_ref_constraint->add_property( iv_principal_property = 'BillingDocument'   iv_dependent_property = 'BillingDocument' )."#EC NOTEXT
* Association Sets for association - FooterData
lo_assoc_set = lo_association->create_assoc_set( iv_assoc_set_name = 'FooterDataSet' ). "#EC NOTEXT
 lo_association = model->create_association(
                            iv_association_name = 'Item' "#EC NOTEXT
                            iv_left_type        = 'BillingDocumentNode' "#EC NOTEXT
                            iv_right_type       = 'ItemData' "#EC NOTEXT
                            iv_right_card       = 'N' "#EC NOTEXT
                            iv_left_card        = '1' ). "#EC NOTEXT
* Referential constraint for association - Item
lo_ref_constraint = lo_association->create_ref_constraint( ).
lo_ref_constraint->add_property( iv_principal_property = 'BillingDocument'   iv_dependent_property = 'BillingDocument' )."#EC NOTEXT
* Association Sets for association - Item
lo_assoc_set = lo_association->create_assoc_set( iv_assoc_set_name = 'ItemSet' ). "#EC NOTEXT


* Navigation Properties for entity - Header
lo_entity_type = model->get_entity_type( iv_entity_name = 'Header' ). "#EC NOTEXT
lo_nav_property = lo_entity_type->create_navigation_property( iv_property_name  = 'BillingDocumentNode' "#EC NOTEXT
                                                          iv_association_name = 'HeaderData' ). "#EC NOTEXT
* Navigation Properties for entity - ItemData
lo_entity_type = model->get_entity_type( iv_entity_name = 'ItemData' ). "#EC NOTEXT
lo_nav_property = lo_entity_type->create_navigation_property( iv_property_name  = 'BillingDocumentNode' "#EC NOTEXT
                                                          iv_association_name = 'Item' ). "#EC NOTEXT
* Navigation Properties for entity - Footer
lo_entity_type = model->get_entity_type( iv_entity_name = 'Footer' ). "#EC NOTEXT
lo_nav_property = lo_entity_type->create_navigation_property( iv_property_name  = 'BillingDocumentNode' "#EC NOTEXT
                                                          iv_association_name = 'FooterData' ). "#EC NOTEXT


   lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
   lo_nav_property = lo_entity_type->create_navigation_property( iv_property_name  = 'HeaderData' "#EC NOTEXT
                                                          iv_association_name = 'HeaderData' ). "#EC NOTEXT
   lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
   lo_nav_property = lo_entity_type->create_navigation_property( iv_property_name  = 'Footer' "#EC NOTEXT
                                                          iv_association_name = 'FooterData' ). "#EC NOTEXT
   lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
   lo_nav_property = lo_entity_type->create_navigation_property( iv_property_name  = 'ItemDataSet' "#EC NOTEXT
                                                          iv_association_name = 'Item' ). "#EC NOTEXT
  endmethod.


  method DEFINE.
*&---------------------------------------------------------------------*
*&           Generated code for the MODEL PROVIDER BASE CLASS          &*
*&                                                                     &*
*&  !!!NEVER MODIFY THIS CLASS. IN CASE YOU WANT TO CHANGE THE MODEL   &*
*&        DO THIS IN THE MODEL PROVIDER SUBCLASS!!!                    &*
*&                                                                     &*
*&---------------------------------------------------------------------*


data:
  lo_entity_type    type ref to /iwbep/if_mgw_odata_entity_typ, "#EC NEEDED
  lo_complex_type   type ref to /iwbep/if_mgw_odata_cmplx_type, "#EC NEEDED
  lo_property       type ref to /iwbep/if_mgw_odata_property, "#EC NEEDED
  lo_association    type ref to /iwbep/if_mgw_odata_assoc,  "#EC NEEDED
  lo_assoc_set      type ref to /iwbep/if_mgw_odata_assoc_set, "#EC NEEDED
  lo_ref_constraint type ref to /iwbep/if_mgw_odata_ref_constr, "#EC NEEDED
  lo_nav_property   type ref to /iwbep/if_mgw_odata_nav_prop, "#EC NEEDED
  lo_action         type ref to /iwbep/if_mgw_odata_action, "#EC NEEDED
  lo_parameter      type ref to /iwbep/if_mgw_odata_property, "#EC NEEDED
  lo_entity_set     type ref to /iwbep/if_mgw_odata_entity_set, "#EC NEEDED
  lo_complex_prop   type ref to /iwbep/if_mgw_odata_cmplx_prop. "#EC NEEDED

* Extend the model
model->extend_model( iv_model_name = 'FDP_V3_BD_STANDARD_GLO_GEN_MDL' iv_model_version = '0001' ). "#EC NOTEXT

model->set_schema_namespace( 'FDP_V3_BD_STANDARD_SRV' ).


*Disable selected properties in a entity type
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'PayerPartyNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'PartnerFunctionNameLangu' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'SoldToPartyNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'PartnerFunctionNameLangu' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'ItemBatchDetailsNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'BillingDocumentItem' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentItemNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'BatchItemBillingVariant' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentItemNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'BillingDocument' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentItemNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'PricingDate' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentItemNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ReturnItemProcessingType' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentItemNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ExchangeRate' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentItemNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ExchangeRateDate' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentItemNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_KDMAT_BDI' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentItemNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_KDMAT_BDIF' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'ItemPricingConditionNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ConditionBaseValueUnit_I' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'ItemPricingConditionNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ConditionRateValueUnit_I' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'BillingSDDocumentCategoryNameLangu' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'BillingDocumentTypeNameLangu' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'SalesOrganizationNameLangu' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_FOBVALUE_BDH' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_FOBVALUE_BDHC' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_BSTDK_BDH' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_KDMAT_BDH' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_HOUSEBANKID_BDH' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_TRANSPORTVENDORCO_BDH' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_BILLFROM_BDH' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_EPCGLICENSENO_BDH' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_SHIPFROM_BDH' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_LRNUMBER_BDH' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_VEHICLETYPE_BDH' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_LRDATE_BDH' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_PORTOFDISCHARGE_BDH' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_VEHICLENUMBER_BDH' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_MODEOFDEL_BDH' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_PORTCODE_BDH' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_BILLDATE_BDH' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_SHIPPINGBILLNUMBER_BDH' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_PORTOFLOADING_BDH' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_VENDORGSTINNUMBER_BDH' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_INVOICEREFERENCE_BDH' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_DISTANCE_BDH' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_SHIPPINGBILLDATE_BDH' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_VEHICLECAPACITY_BDH' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_RODTEPLICENSENO_BDH' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_TRANSPORTVENDORGST_BDH' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_RODTEPLICENSENO_BDHF' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_HOUSEBANKID_BDHF' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_HOUSEBANKID_BDHT' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_INVOICEREFERENCE_BDHF' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_SHIPPINGBILLDATE_BDHF' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_PORTOFDISCHARGE_BDHF' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_PORTOFDISCHARGE_BDHT' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_TRANSPORTVENDORCO_BDHF' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_TRANSPORTVENDORCO_BDHT' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_SHIPFROM_BDHF' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_SHIPFROM_BDHT' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_VEHICLETYPE_BDHF' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_VEHICLETYPE_BDHT' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_SHIPPINGBILLNUMBER_BDHF' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_MODEOFDEL_BDHF' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_MODEOFDEL_BDHT' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_KDMAT_BDHF' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_PORTOFLOADING_BDHF' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_PORTOFLOADING_BDHT' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_TRANSPORTVENDORGST_BDHF' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_LRDATE_BDHF' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_BSTDK_BDHF' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_FOBVALUE_BDHF' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_FOBVALUE_BDHT' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_VEHICLENUMBER_BDHF' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_EPCGLICENSENO_BDHF' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_BILLFROM_BDHF' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_BILLFROM_BDHT' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_VEHICLECAPACITY_BDHF' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_VEHICLECAPACITY_BDHT' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_PORTCODE_BDHF' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_PORTCODE_BDHT' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_DISTANCE_BDHF' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_VENDORGSTINNUMBER_BDHF' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_BILLDATE_BDHF' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillingDocumentNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ZZ1_LRNUMBER_BDHF' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'BillToPartyNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'PartnerFunctionNameLangu' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'ShipToPartyNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'PartnerFunctionNameLangu' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'PricingConditionNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ConditionBaseValueUnit_I' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'PricingConditionNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'ConditionRateValueUnit_I' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
try.
lo_entity_type = model->get_entity_type( iv_entity_name = 'ItemShipToPartyNode' ). "#EC NOTEXT
lo_property    = lo_entity_type->get_property( iv_property_name = 'PartnerFunctionNameLangu' ). "#EC NOTEXT
lo_property->set_disabled( iv_disabled = abap_true ).
CATCH /iwbep/cx_mgw_med_exception.
*  No Action was taken as the OData Element is not a part of redefined service
ENDTRY.
* New artifacts have been created in the service builder after the redefinition of service
create_new_artifacts( ).
* Labels of the artifacts have been changed in the service builder after the redefinition of service
change_labels( ).
  endmethod.


  method GET_EXTENDED_MODEL.
*&---------------------------------------------------------------------*
*&           Generated code for the MODEL PROVIDER BASE CLASS          &*
*&                                                                     &*
*&  !!!NEVER MODIFY THIS CLASS. IN CASE YOU WANT TO CHANGE THE MODEL   &*
*&        DO THIS IN THE MODEL PROVIDER SUBCLASS!!!                    &*
*&                                                                     &*
*&---------------------------------------------------------------------*



ev_extended_service  = 'FDP_V3_BD_STANDARD_GLO_GEN_SRV'.                "#EC NOTEXT
ev_ext_service_version = '0001'.               "#EC NOTEXT
ev_extended_model    = 'FDP_V3_BD_STANDARD_GLO_GEN_MDL'.                    "#EC NOTEXT
ev_ext_model_version = '0001'.                   "#EC NOTEXT
  endmethod.


  method GET_LAST_MODIFIED.
*&---------------------------------------------------------------------*
*&           Generated code for the MODEL PROVIDER BASE CLASS          &*
*&                                                                     &*
*&  !!!NEVER MODIFY THIS CLASS. IN CASE YOU WANT TO CHANGE THE MODEL   &*
*&        DO THIS IN THE MODEL PROVIDER SUBCLASS!!!                    &*
*&                                                                     &*
*&---------------------------------------------------------------------*


  constants: lc_gen_date_time type timestamp value '20251126102943'. "#EC NOTEXT
rv_last_modified = super->get_last_modified( ).
IF rv_last_modified LT lc_gen_date_time.
  rv_last_modified = lc_gen_date_time.
ENDIF.
  endmethod.


  method LOAD_TEXT_ELEMENTS.
*&---------------------------------------------------------------------*
*&           Generated code for the MODEL PROVIDER BASE CLASS          &*
*&                                                                     &*
*&  !!!NEVER MODIFY THIS CLASS. IN CASE YOU WANT TO CHANGE THE MODEL   &*
*&        DO THIS IN THE MODEL PROVIDER SUBCLASS!!!                    &*
*&                                                                     &*
*&---------------------------------------------------------------------*


data:
  lo_entity_type    type ref to /iwbep/if_mgw_odata_entity_typ,           "#EC NEEDED
  lo_complex_type   type ref to /iwbep/if_mgw_odata_cmplx_type,           "#EC NEEDED
  lo_property       type ref to /iwbep/if_mgw_odata_property,             "#EC NEEDED
  lo_association    type ref to /iwbep/if_mgw_odata_assoc,                "#EC NEEDED
  lo_assoc_set      type ref to /iwbep/if_mgw_odata_assoc_set,            "#EC NEEDED
  lo_ref_constraint type ref to /iwbep/if_mgw_odata_ref_constr,           "#EC NEEDED
  lo_nav_property   type ref to /iwbep/if_mgw_odata_nav_prop,             "#EC NEEDED
  lo_action         type ref to /iwbep/if_mgw_odata_action,               "#EC NEEDED
  lo_parameter      type ref to /iwbep/if_mgw_odata_property,             "#EC NEEDED
  lo_entity_set     type ref to /iwbep/if_mgw_odata_entity_set.           "#EC NEEDED


DATA:
     ls_text_element TYPE ts_text_element.                   "#EC NEEDED


clear ls_text_element.
ls_text_element-artifact_name          = 'BillingDocument'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'BillToPartyNode'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '001'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'BillingDocument'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'IncotermsNode'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '002'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'BillingDocument'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ItemPricingConditionNode'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '003'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'BillingDocumentItem'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ItemPricingConditionNode'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '004'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'BillingDocument'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ItemShipToPartyNode'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '005'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'BillingDocumentItem'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ItemShipToPartyNode'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '006'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'BillingDocument'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ItemTextElementNode'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '007'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'BillingDocumentItem'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ItemTextElementNode'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '008'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'BillingDocument'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'LegallyRequiredTextNode'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '009'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'BillingDocument'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'PayerPartyNode'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '010'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'BillingDocument'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'PaymentMethodNode'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '011'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'BillingDocument'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'PaymentTermsNode'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '012'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'BillingDocument'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'PricingConditionNode'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '013'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'BillingDocument'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'PricingTermsNode'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '014'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'BillingDocument'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ShipToPartyNode'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '015'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'BillingDocument'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'SoldToPartyNode'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '016'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'BillingDocument'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'TaxationTermsNode'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '017'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'BillingDocument'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'TextElementNode'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '018'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'BillingDocument'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'VATSummaryNode'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '019'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'BillingDocument'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '020'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'Invoice'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '021'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'InvoiceDate'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '022'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'Reference'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '023'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'Taxno'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '024'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'CustomerPoNo'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '025'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'CustomerPoDate'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '026'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'PaymentTerms'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '027'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'PaymentTermsDescription'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '028'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'IncoTerms'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '029'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'BillFromPlant'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '030'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'BillFromAddress'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '031'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'BillFromGST'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '032'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'BillFromPan'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '033'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'BillFromIec'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '034'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'BillFromIecDt'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '131'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'BillFromStatecode'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '035'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'BillFromSuppCode'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '036'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'BillFromCin'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '037'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'BillToCustomerCode'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '038'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'BillToAddress'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '039'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'BillToGST'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '040'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'BillToPan'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '041'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'BillToIec'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '042'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'BillToStatecode'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '043'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'BillToCin'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '044'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'ShipfromPlant'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '045'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'ShipfromAddress'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '046'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'ShipfromGST'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '047'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'ShipfromPan'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '048'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'ShipfromIec'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '049'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'ShipfromIecDt'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '132'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'ShipfromStatecode'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '050'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'ShipfromCin'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '051'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'ShipToCustomeCode'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '052'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'ShipToAddress'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '053'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'ShipToGST'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '054'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'ShipToPan'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '055'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'ShipToIec'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '056'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'ShipToStatecode'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '057'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'ShipToCin'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '058'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'VendorCode'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '059'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'TransporterName'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '060'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'TransporterGstin'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '061'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'ModeofDelivery'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '062'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'Vehicletype'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '063'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'VehicleNo'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '064'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'Distance'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '065'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'LrdocketNo'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '066'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'LrdocketDate'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '067'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'Remarks'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '068'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'IRN'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '069'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'EwayBillNo'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '070'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'EwayBillDate'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '071'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'TaxableValue'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '072'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'CustomerJob'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '073'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'LutDate'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '126'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'LutNo'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '127'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'Financialyear'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '128'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'CommercialInvNo'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '129'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'CommercialDate'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '130'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'Einv'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '133'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'TypeofExport'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '134'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'LicenceNumber'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'HEADERDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '135'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'BillingDocument'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '074'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'MaterialCode'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '075'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'MaterialCodeDescription'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '076'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'CustomerMaterialCode'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '077'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'CustomerMaterialDescription'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '078'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'HsnSac'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '079'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'Uom'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '080'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'Quntity'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '081'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'UnitPrise'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '082'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'Discount'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '083'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'DiscValue'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '084'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'ValueafterDiscount'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '085'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'TotalBasicValue'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '086'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'TotalDiscount'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '087'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'Value'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '088'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'FreightCharges'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '089'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'PackagingCharges'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '090'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'ToolAmortizationCharges'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '091'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'TaxableValue'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '092'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'Igst'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '093'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'IgstValue'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '094'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'Cgst'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '095'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'CgstValue'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '096'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'SgstValue'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '097'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'Sgst'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '098'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'TcsValue'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '099'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'Tcs'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '100'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'TotalInvoiceValue'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '101'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'IgstTot'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '102'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'IgstValueTot'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '103'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'CgstTot'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '104'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'CgstValueTot'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '105'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'SgstValueTot'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '106'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'SgstTot'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '107'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'TcsValueTot'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '108'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'TcsTot'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '109'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'EmptyValue'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '110'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'GSTamtwords'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '111'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'Invamtwords'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '112'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'Value2'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '113'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'TotalBasic'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '114'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'EInvoiceQRC'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '115'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'LessTaxablevalue'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '116'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'CustomerQRC'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '117'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'EmptyValueQRC'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '118'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'HSNDescription'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '119'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'QRCCustomer'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'ITEMDATA'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '120'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'BillingDocument'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'FOOTER'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '121'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'Name'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'FOOTER'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '122'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'Value'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'FOOTER'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '123'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'NameSign'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'FOOTER'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '124'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
clear ls_text_element.
ls_text_element-artifact_name          = 'NameSignVal'.      "#EC NOTEXT
ls_text_element-artifact_type          = 'PROP'.                       "#EC NOTEXT
ls_text_element-parent_artifact_name   = 'FOOTER'.     "#EC NOTEXT
ls_text_element-parent_artifact_type   = 'ETYP'.                             "#EC NOTEXT
ls_text_element-text_symbol            = '125'.         "#EC NOTEXT
APPEND ls_text_element TO rt_text_elements.
  endmethod.
ENDCLASS.
************************************************************************************************************************

CLASS zcl_zexporttaxinv_mpc_ext DEFINITION
  PUBLIC
  INHERITING FROM zcl_zexporttaxinv_mpc
  CREATE PUBLIC .

  PUBLIC SECTION.

    TYPES : BEGIN OF ty_footerdata,
              billingdocument      TYPE vbeln,
              posnr                TYPE posnr,
              unitprice            TYPE string,
              quntity              TYPE string,
              totalbasic           TYPE kbetr,
              dist                 TYPE kbetr,
              discount             TYPE string,
              footerdiscountsval   TYPE kwert,
              footerdiscountsvalue TYPE kwert,
              footerdisval         TYPE kwert,
              disval               TYPE netwr,
              taxablevalue         TYPE kbetr,
              discountval          TYPE kwert,
              freight              TYPE kbetr,
              packing              TYPE kbetr,
              toolamortization     TYPE kbetr,
              igst                 TYPE string,
              igstval              TYPE p LENGTH 16 DECIMALS 3,
              igst_tot             TYPE string,
              igstval_tot          TYPE kbetr,
              lesstaxablevalue     TYPE kbetr,

            END OF ty_footerdata.

    TYPES:
tt_footertable TYPE TABLE OF ty_footerdata WITH EMPTY KEY .
protected section.
private section.
ENDCLASS.



CLASS ZCL_ZEXPORTTAXINV_MPC_EXT IMPLEMENTATION.
ENDCLASS.
********************************************************************************
