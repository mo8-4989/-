markdown
graph TD
    A[開始] --> B{要求ファイル数チェック};
    B -- 3つ以内 --> C{ファイル状態確認};
    B -- 3つ超 --> D[エラーメッセージ返却];
    C -- 全て貸出可能 --> E[ファイル貸出処理];
    C -- 一つでも貸出中 --> F[リクエスト保留];
    E --> G[ファイル状態更新 (貸出中)];
    F --> H[保留キューに追加];
    I[ファイル返却処理] --> J[ファイル状態更新 (貸出可能)];
    J --> K{保留キュー確認};
    K -- リクエストあり --> L[保留キューから処理];
    K -- リクエストなし --> M[終了];
    L --> C;
    G --> M;
    D --> M;
