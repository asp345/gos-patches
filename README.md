# GrapheneOS에 VoLTE 패치 스크립트 추가하기

adevtool로 vendor file들을 다운로드 받은 이후,  vendor/google_devices/<codename>/ 디렉토리 내의 다음 파일들을 수정하면 됩니다. codename은 픽셀 8 (shiba) 기준입니다.

1. shiba.mk 마지막에 다음 내용 추가
```
PRODUCT_COPY_FILES += \
    vendor/google_devices/shiba/write_at_cmd.sh:vendor/bin/write_at_cmd.sh
```

2. write_at_cmd.sh 새로 작성 (아래 내용은 LGU+ SIM1 기준)
```
#!/vendor/bin/sh

sleep 5

echo -e 'AT+GOOGSETNV="UL3.Cap.Phych.supp_of_fdpch",0,"01,00,00,00"\r
AT+GOOGSETNV="UL3.Cap.Phych.supp_of_Efdpch",0,"01,00,00,00"\r
AT+GOOGSETNV="UL3.Cap.Phych.supp_ul_dtx",0,"00"\r
AT+GOOGSETNV="UL3.Cap.Phych.slotFormat4",0,"00,00,00,00"\r
AT+GOOGSETNV="UL3.Cap.Multi.supp_IRAT PS HO to E-UTRA",0,"01"\r
AT+GOOGSETNV="UL3.Cap.MultiCellSupport_DC_HSDPA",0,"01"\r
AT+GOOGSETNV="UL3.Etc.FastDormancyT323Rel8Support",0,"01,00,00,00"\r

AT+GOOGSETNV="UECAPA_INTRA_FREQ_SI_ACQ_FOR_HO",0,"01"\r
AT+GOOGSETNV="UECAPA_INTER_FREQ_SI_ACQ_FOR_HO",0,"01"\r
AT+GOOGSETNV="UECAPA_UTRAN_SI_ACQ_FOR_HO",0,"01"\r
AT+GOOGSETNV="UECAPA_PDCP_ROHC_PROFILES",3,"00"\r

AT+GOOGSETNV="UECAPA_REL10_FOURLAYER_TM3TM4",0,"01"\r
AT+GOOGSETNV="UECAPA_REL10_ORIG_FOURLAYER_TM3TM4",0,"01"\r
AT+GOOGSETNV="UECAPA_REL10_CA_INDEX",0,"01,00,00,00"\r
AT+GOOGSETNV="UECAPA_REL10_MIMO_CAPA_DL",0,"01"\r
AT+GOOGSETNV="UECAPA_REL10_MIMO_CAPA_UL",0,"02"\r
AT+GOOGSETNV="UECAPA_REL10_MODIFIED_MPR_BEHAVIOR",0,"00,00,00,C0"\r
AT+GOOGSETNV="UECAPA_REL10_FGI103",0,"01"\r

AT+GOOGSETNV="UECAPA_REL12_EXTENDED_MAX_MEASID_SUPPORT",0,"01"\r

AT+GOOGSETNV="UECAPA_REL14_DIFF_FALLBACKCOMB",0,"01"\r

AT+GOOGSETNV="NR.CONFIG.MODE",0,"01"\r
AT+GOOGSETNV="NR.ENDC.MODE",0,"11"\r
AT+GOOGSETNV="DS.NR.CONFIG.MODE",0,"01"\r
AT+GOOGSETNV="DS.NR.ENDC.MODE",0,"11"\r

AT+GOOGSETNV="NASU.NR.CONFIG.MODE",0,"01"\r
AT+GOOGSETNV="DS.NASU.NR.CONFIG.MODE",0,"01"\r

AT+GOOGSETNV="!NRCAPA.Switch.DssFeature",0,"01"\r
AT+GOOGSETNV="!NRCAPA.Gen.DynamicPowerSharing",0,"01"\r

AT+GOOGSETNV="PSS.AIMS.DYNAMIC_OPERATORSPEC_FLAG",0,"01"\r
AT+GOOGSETNV="PSS.AIMS.ENABLE.RPORT-InVia-Header",0,"01"\r

AT+GOOGSETNV="PSS.AIMS.Payload-EVS",0,"6E"\r
AT+GOOGSETNV="PSS.AIMS.Audio.Media.RS",0,"00,00,00,00"\r
AT+GOOGSETNV="PSS.AIMS.Audio.Media.RR",0,"20,03,00,00"\r

AT+GOOGSETNV="DS.PSS.AIMS.Payload-EVS",0,"6E"\r
AT+GOOGSETNV="DS.PSS.AIMS.Audio.Media.RS",0,"00,00,00,00"\r
AT+GOOGSETNV="DS.PSS.AIMS.Audio.Media.RR",0,"20,03,00,00"\r

AT+GOOGSETNV="DS.PSS.AIMS.ENABLE.RPORT-InVia-Header",0,"01"\r
AT+GOOGSETNV="DS.PSS.AIMS.DYNAMIC_OPERATORSPEC_FLAG",0,"01"\r
AT+GOOGSETNV="DS.PSS.AIMS.ACCESSTYPE.SUPPORT",0,"00"\r

AT+GOOGSETNV="!NRSM.MsSupportLocalAddrTFTRequest",0,"01"\r

AT+GOOGSETNV="!SAEL3.PCO_IPV4_MTU_MAX_SIZE",0,"DC,05"\r
AT+GOOGSETNV="!SAEL3.IMS_PCO_IPV4_MTU_MAX_SIZE",0,"DC,05"\r
AT+GOOGSETNV="!SAEL3.EXTPCO_REQUEST",0,"01"\r
AT+GOOGSETNV="!SAEL3.ENABLE_GUARD_T_FOR_WAIT_ATTACHAPN",0,"01"\r
AT+GOOGSETNV="!SAEL3.DISABLE_IPV4_MTU_IN_PCO",0,"01"\r
AT+GOOGSETNV="!SAEL3.Dual_IP_PDP",0,"01"\r
AT+GOOGSETNV="!SAEL3.PDN_SM_PDU_DN_REQ_CONTAINER",0,"00"\r
AT+GOOGSETNV="!SAEL3_DS.PCO_IPV4_MTU_MAX_SIZE",0,"DC,05"\r
AT+GOOGSETNV="!SAEL3_DS.IMS_PCO_IPV4_MTU_MAX_SIZE",0,"DC,05"\r
AT+GOOGSETNV="!SAEL3_DS.EXTPCO_REQUEST",0,"01"\r
AT+GOOGSETNV="!SAEL3_DS.ENABLE_GUARD_T_FOR_WAIT_ATTACHAPN",0,"01"\r
AT+GOOGSETNV="!SAEL3_DS.DISABLE_IPV4_MTU_IN_PCO",0,"01"\r

AT+GOOGSETNV="HCOMMON.MM.LCS_VA_capability",0,"01"\r

AT+GOOGSETNV="NASL3.MM.umts_fdd",0,"01"\r
AT+GOOGSETNV="NASL3.MM.GeranFeaturePack1",0,"01"\r
AT+GOOGSETNV="NASL3.MM.gea_algorithms",1,"00"\r
AT+GOOGSETNV="NASL3.SM.NW Initiated Secondary PDP Activation Support",0,"01"\r
AT+GOOGSETNV="ds_NASL3.MM.umts_fdd",0,"01"\r
AT+GOOGSETNV="ds_NASL3.MM.GeranFeaturePack1",0,"01"\r
AT+GOOGSETNV="ds_NASL3.MM.gea_algorithms",1,"00"\r

AT+CFUN=0\rAT+CFUN=1\r' > /dev/umts_router

echo -e 'AT+GOOGSETNV="PSS.AIMS.Payload-AMRWB",0,"64"\r
AT+GOOGSETNV="PSS.AIMS.Payload-AMRWB",1,"FF"\r
AT+GOOGSETNV="PSS.AIMS.Payload-AMRNB",1,"FF"\r
AT+GOOGSETNV="PSS.AIMS.Payload-DTMF",0,"65"\r
AT+GOOGSETNV="PSS.AIMS.Payload-DTMF.WB",0,"6B"\r
AT+GOOGSETNV="PSS.AIMS.Audio.Media.RR",0,"9C,04,00,00"\r

AT+GOOGSETNV="DS.PSS.AIMS.Payload-AMRWB",0,"64"\r
AT+GOOGSETNV="DS.PSS.AIMS.Payload-AMRWB",1,"FF"\r
AT+GOOGSETNV="DS.PSS.AIMS.Payload-AMRNB",1,"FF"\r
AT+GOOGSETNV="DS.PSS.AIMS.Payload-DTMF",0,"65"\r
AT+GOOGSETNV="DS.PSS.AIMS.Payload-DTMF.WB",0,"6B"\r
AT+GOOGSETNV="DS.PSS.AIMS.Audio.Media.RR",0,"9C,04,00,00"\r

AT+CFUN=0\rAT+CFUN=1\r' > /dev/umts_router
log -t VoLTE-Config "Korea VoLTE Script finished successfully."
```

3. sepolicy/vendor/file_contexts에 다음 내용 추가
```
/vendor/bin/write_at_cmd.sh   u:object_r:write_at_cmd_exec:s0
```

4. sepolicy/vendor/write_at_cmd.te 새로 작성
```
type write_at_cmd, domain;
type write_at_cmd_exec, exec_type, vendor_file_type, file_type;
init_daemon_domain(write_at_cmd)
allow write_at_cmd radio_device:chr_file { rw_file_perms ioctl };
allow write_at_cmd logd:fd use;
allow write_at_cmd logd_socket:sock_file write;
allow shell write_at_cmd_exec:file getattr;
allow write_at_cmd shell_exec:file execute_no_trans;
allow write_at_cmd toolbox_exec:file { read getattr execute open };
get_prop(write_at_cmd, telephony_status_prop)
allow write_at_cmd vendor_toolbox_exec:file { execute execute_no_trans read open };
```

5. proprietary/vendor/etc/init/init.pixel.rc 에 다음 내용 추가
```
service write_at_cmd /vendor/bin/write_at_cmd.sh
    class main
    user system
    group system
    oneshot
    disabled

on property:sys.boot_completed=1
    setprop persist.dbg.volte_avail_ovr 1
    start write_at_cmd
```

위 5가지 적용 후 빌드 진행하면 부팅 완료 후 패치 스크립트가 실행되게 됩니다.
