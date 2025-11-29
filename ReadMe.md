### Interface 2023年7月号 特集「ゼロから作るOS」配布プログラムを使用してRTOSの学習をする

1. 起動処理について
   メモリセクションの初期化について\n
   以下のコードで起動処理時のメモリセクションの初期化をしている。
   主な処理はROMに保存されているグローバル変数をRAMに移動することと変数のみの宣言時に0で初期化をすること。
   ```c
    static void init_section(void)
    {
        _UW     *src, *top, *end;
        INT     i;
    
        /* dataセクションの初期化 (rodataからdataへコピー) */
        src = (_UW*)&__data_org;;
        top = (_UW*)&__data_start;
        end = (_UW*)&__data_end;
        while(top != end) {
            *top++ = *src++;
        }
    
        /* bssセクションの初期化 （0クリア） */
        for(i = ((int)&__bss_end - (int)&__bss_start)/sizeof(int); i > 0 ; i--) {
            *top++ = 0;
        }
    }
   ```




