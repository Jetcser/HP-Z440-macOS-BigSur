˵��:
OpenCore�汾0.7.6���༭config.list�Ƽ�ProperTree�������OCC�����ʹ�ö�Ӧ�汾��

Ӳ����
ƽ̨��HP Z440 ��X99��
��������E5-1650v3 ��Haswell-E��
�Կ���Nvdia Quadro K4200 (GK104��
����������Fenvi BCD94360CD
ϵͳӲ�̣�Intel S3610 200GB ��SATA��
����Ӳ�̣�Toshiba P300 3TB (exFAT��
macOS�汾��Catalina 10.5.7

ACPI��
1.Z440��BIOS�汾���µ����°��2.57��
2.SSDT-EC-Z440.aml ֻ�Ƿ�ðEC�豸��Z440��ACPI��û���ҵ�EC�豸��
3.SSDT-HPET.aml ʹ��SSDTTime���ɵģ���Ҫ���IRQ�жϵ����⣬�Ա�ԭʼACPI��֮���֣�ԭ���ǰ�RTC�豸IRQ8��TMR�豸��IRQ0ȥ�������õ�HPET�豸�ϣ���Ȼ���������л�Kernel Panic��Ҫ���config.plist�ϵ�APCI->Patchʹ�ã������ˡ�
4.SSDT-PLUG-Z440.aml ���CPU��Դ���Ƶ���⣬ͬʱҪ��config.plist����Kernel->Emulate->Cpuid1Data�аѷ�ðID��ã�����CPU�ķ�ð����ȥ��һ�¾�֪���ˣ�����E5-1650v3�ܹ���Haswell-E����ȥ������ܹ���Ӧ�ķ�ðID��
5.SSDT-RTC0-RANGE-Z440.aml RTC�������������������� -.-��
6.SSDT-UNC.aml ͨ�õ�UNC�������������ò�dortania.github.io��
7.SSDT-MEM2-add.aml��SSDT-SLPB-add.aml��SSDT-SMBUS-MCHC-add.aml���Լ��ӵģ���ð�⼸���豸�ã������ò��ö��ܿ������пտ����Լ��о��¡�

Kernel��
�ⲿ�־��ǳ��õ���ЩKexts������Lilu��Whatevergreen��VirtualSMC����������AppleALC������Intel��������֮�࣬��Щ����ͨ�õģ�����׸����

��Ҫע�����USB�˿ڶ��ƣ�Z440��X99ƽ̨�����Ѿ����ƺ��ˣ��ļ�����USBMap.kext��Ĭ�϶�Ӧ����iMacPro1,1��������û���MacPro6,1�����������ļ�����Ӧ���ļ�����Kexts->off��
  ������Լ����ֵĻ��������򵥵ķ�ʽ����Windows����USBToolbox�����������巽���μ���
https://heipg.cn/tutorial/customize-usb-port-windows.html��

NVRAM��

boot-args���� npci=0x2000 alcid=11 -v

npci=0x2000��X99ƽ̨����ġ�

alcid��AppleALC������Ҫ�ģ�����Z440��������������ALC221��layout-id��11��

-v�ǿ����ַ�ģʽ������������ʾ�����ַ���Ϣ�������Ŵ���װ����ȥ����ȥ��֮����ҪReset NVRAM����Ч��

PlatformInfo��
  
���Ͳ��õ���iMacPro1,1�����Ѿ������к�ɶ��ɾ���ˣ�����Ҫ��OCC����������Ӧ�����кš�
�������������������������Fenvi-BCM94360CD������¼AppleID�Ļ�������Ҫ������MAC������ROM��
�����https://heipg.cn/tutorial/macserial-and-iservice-opencore.html

  ������Ҫע����ǣ�KextsĿ¼�����USB�˿ڶ����ļ�USBMap.kext�Ƕ�Ӧ���͵ġ�
  ���������Ļ���Ҳ������MacPro6,1����Ҫ��ǿ��һ�µ��ǣ�ע�������Ӧ��USBMap.kext�������汾���ļ�����Kexts->off���棬�õ�ʱ���һ���������ˡ�


*����֪ʶ��ѯdortania.github.io