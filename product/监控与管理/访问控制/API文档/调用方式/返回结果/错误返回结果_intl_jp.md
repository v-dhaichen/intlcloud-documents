APIの呼び出しが失敗した場合、最後に返された結果のエラーコードcodeは0ではなく、エラーコードが表示されて、messageフィールドに詳細なエラーメッセージが表示されます。ユーザーは、codeとmessageに基づいて[エラーコード]ページで具体的なエラーメッセージを確認できます。
返されたエラーの例は次の通りです。
```
{
    "code": 4000,
    "message": "(100004)projectIdが正しくない",
}
```

