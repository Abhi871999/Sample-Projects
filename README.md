# Sample-Projects
REPORT z_mm_po_report.

"Selection Screen
PARAMETERS: p_ebeln TYPE ekko-ebeln OBLIGATORY. "Purchase Order Number

"Internal Tables
DATA: lt_po_header TYPE TABLE OF ekko,  "Header Data
      lt_po_items  TYPE TABLE OF ekpo,  "Item Data
      wa_po_header TYPE ekko,
      wa_po_item   TYPE ekpo.

"Fetch PO Header Data
SELECT * FROM ekko INTO TABLE lt_po_header WHERE ebeln = p_ebeln.

"Check if PO Exists
IF lt_po_header IS INITIAL.
  WRITE: / 'No Purchase Order found for the given number'.
  EXIT.
ENDIF.

"Fetch PO Item Data
SELECT * FROM ekpo INTO TABLE lt_po_items WHERE ebeln = p_ebeln.

"Display Header Data
LOOP AT lt_po_header INTO wa_po_header.
  WRITE: / 'Purchase Order:', wa_po_header-ebeln,
         / 'Vendor:', wa_po_header-lifnr,
         / 'Document Date:', wa_po_header-bedat.
ENDLOOP.

"Display Item Data
WRITE: / '---- Purchase Order Items ----'.
LOOP AT lt_po_items INTO wa_po_item.
  WRITE: / 'Material:', wa_po_item-matnr,
         'Quantity:', wa_po_item-menge,
         'Net Price:', wa_po_item-netpr.
ENDLOOP.
