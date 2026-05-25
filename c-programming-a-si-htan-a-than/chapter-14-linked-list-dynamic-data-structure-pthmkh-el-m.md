---
chapter: 14
title: "Linked List — Dynamic Data Structure ပထမခြေလှမ်း"
generated_at: "2026-05-25T21:55:57.869240+00:00"
---

# Chapter 14: Linked List — Dynamic Data Structure ပထမခြေလှမ်း

## ၁။ မိတ်ဆက်နှင့် နောက်ခံအကြောင်းအရာ (Introduction and Background)

ကွန်ပျူတာ သိပ္ပံနှင့် ပရိုဂရမ်မင်းလောကတွင် Data structure များသည် အလွန်အရေးကြီးသော အခြေခံဖြစ်သည်။ ကျွန်ုပ်တို့သည် Data များကို မည်သို့ သိမ်းဆည်းမည်၊ မည်သို့ စီမံခန့်ခွဲမည်ကို ဆုံးဖြတ်သည့် အခြေခံ မူဘောင်များ (frameworks) ဖြစ်ကြသည်။ ထို Data structure များအနက် Array များသည် အလွယ်တကူ အသုံးပြုနိုင်သော နည်းလမ်းတစ်ခုဖြစ်သော်လည်း ၎င်းတို့တွင် အကန့်အ制限များ ရှိသည်။

### Array များ၏ အားနည်းချက်များ

Array များသည် Data များကို တစ်ဆက်တည်း၊ အတူတူနေရာတွင် သိမ်းဆည်းထားသည့် အလွန်ထိရောက်သော နည်းလမ်းတစ်ခုဖြစ်သည်။ ၎င်းတို့၏ အားသာချက်မှာ အချက်အလက်များကို အလွန်လျင်မြန်စွာ ဝင်ရောက်ကြည့်ရှုနိုင်ခြင်း (Random Access) ဖြစ်သည်။ သို့သော် Array များတွင် အဓိကအားဖြင့် အားနည်းချက် နှစ်ခု ရှိသည်။ ပထမတစ်ခုမှာ **Fixed Size** (အမြဲတမ်း သတ်မှတ်ထားသော အရွယ်အစား) ဖြစ်ခြင်းပင် ဖြစ်သည်။ Array တစ်ခုကို ဖန်တီးသည့်အခါ ၎င်း၏ အရွယ်အစားကို ကြိုတင်သတ်မှတ်ရမည်ဖြစ်ပြီး ထိုအရွယ်အစားထက် ပို၍ သို့မဟုတ် လျော့၍ Data ထည့်ရန် မဖြစ်နိုင်ပေ။ Data များ ထပ်ထည့်ရန် သို့မဟုတ် ဖယ်ရှားရန် လိုအပ်လာသည့်အခါ Array ၏ အရွယ်အစားကို ပြန်လည်သတ်မှတ်၍ အခြားနေရာသို့ ပြောင်းရွှေ့ခြင်း (reallocation) စသည့် ရှုပ်ထွေးသော လုပ်ငန်းစဉ်များ လိုအပ်လာသည်။

ဒုတိယအချက်မှာ **Insertion နှင့် Deletion များ၏ ရှုပ်ထွေးမှု** ဖြစ်သည်။ Array ၏ အလယ်တွင် Data အသစ် ထည့်ရန် သို့မဟုတ် Data တစ်ခုကို ဖယ်ရှားရန် လိုအပ်သည့်အခါ၊ ထိုနေရာမှ နောက်ဆက်တွဲရှိ Data အားလုံးကို နောက်တစ်နေရာသို့ ရွှေ့ပြောင်းရမည် ဖြစ်သည်။ ဤလုပ်ငန်းစဉ်သည် Array ၏ အလယ်တွင် ရှိနေသည့် Data များအားလုံးကို ပြန်လည်ရွှေ့ပြောင်းရသောကြောင့် အချိန်ကုန်ပြီး ရှုပ်ထွေးမှုများစွာ ဖြစ်ပေါ်စေသည်။ ဥပမာအားဖြင့်၊ အရှေ့ဘက်ရှိ Data ၁၀၀၀ ကို နောက်တစ်နေရာသို့ ရွှေ့ပြောင်းရမည်ဆိုလျှင် ထိုအချိန်သည် $O(n)$ (n သည် Data အရေအတွက်) အချိန်ယူရမည် ဖြစ်သည်။

### Linked List ၏ မိတ်ဆက်

ဤ Array များ၏ ကန့်သတ်ချက်များကို ကျော်လွှားရန်အတွက် **Dynamic Data Structure** များ၏ လိုအပ်ချက် ပေါ်ပေါက်လာသည်။ ဤနေရာတွင် **Linked List** (ချိတ်ဆက်ထားသော စာရင်း) သည် ထင်ရှားသော အဖြေတစ်ခု ဖြစ်လာသည်။ Linked List ဆိုသည်မှာ Data များကို တစ်ဆက်တည်း နေရာတွင် သိမ်းဆည်းမည့်အစား၊ Data တစ်ခုချင်းစီကို **Node** များအဖြစ် ခွဲခြားပြီး ထို Node များအား **pointer** များဖြင့် တစ်ခုနှင့်တစ်ခု ချိတ်ဆက်ထားသည့် နည်းလမ်းဖြစ်သည်။ ဤနည်းလမ်းကို **self-referential struct** (ကိုယ်တိုင်ကို ညွှန်ပြသော struct) ဟုလည်း ခေါ်ဆိုကြသည်။ ဆိုလိုသည်မှာ Node တစ်ခုစီတိုင်းတွင် ထို Node ၏ နောက်ဆက်တွဲ Node ၏ လိပ်စာ (address) ကို သိမ်းဆည်းထားသည့် Pointer တစ်ခု ပါဝင်သည်။

Array နှင့် Linked List ၏ Memory တွင် Data များ သိမ်းဆည်းပုံကို နှိုင်းယှဉ်ကြည့်လျှင် ကြီးမားသော ကွာခြားချက်များ ရှိသည်။ Array များသည် Memory ၏ ရေစီးကြောင်းအတိုင်း (contiguous memory) အတူတူနေရာတွင် သိမ်းဆည်းထားသည်။ ဥပမာအားဖြင့်၊ အိမ်တစ်အိမ်စီကို တစ်ဆက်တည်း လမ်းကြောင်းအတိုင်း ဆက်တိုက်တည်ဆောက်ထားသကဲ့သို့ ဖြစ်သည်။ ဆန့်ကျင်ဘက်အားဖြင့် Linked List များသည် Memory ၏ မည်သည့်နေရာတွင်မဆို လွတ်လပ်စွာ ခွဲခြား၍ သိမ်းဆည်းနိုင်ပြီး၊ ထို Data များအား Pointer များဖြင့် ချိတ်ဆက်ထားသည်။ ၎င်းသည် Memory ကို လွတ်လပ်စွာ အသုံးပြုနိုင်စေပြီး Dynamic ဖြစ်စေသည်။

ဤအခန်းတွင် ကျွန်ုပ်တို့သည် Linked List ၏ အခြေခံအယူအဆများကို လေ့လာပြီး၊ ၎င်းကို C Programming ဖြင့် မည်သို့ အကောင်အထည်ဖော်ရမည်ကို အသေးစိတ် လေ့လာသွားကြမည် ဖြစ်သည်။

## ၂။ Singly Linked List (တစ်လမ်းသွား ချိတ်ဆက်ထားသော စာရင်း)

Singly Linked List (တစ်လမ်းသွား ချိတ်ဆက်ထားသော စာရင်း) သည် Linked List ၏ အခြေခံပုံစံဖြစ်သည်။ ၎င်းသည် Data များအား စဉ်ဆက်မပြတ် ချိတ်ဆက်ထားသော စာရင်းတစ်ခုကို ဖော်ပြသည်။

### Node ဖွဲ့စည်းပုံ (Structure)

Linked List ၏ အခြေခံအုတ်မြစ်မှာ **Node** (သော့) ဖြစ်သည်။ Node တစ်ခုသည် အချက်အလက် (Data) တစ်ခုနှင့် ထို Node မှ နောက်ဆက်တွဲ Node သို့ မည်သို့သွားမည်ကို ညွှန်ပြသည့် Pointer တစ်ခုကို ပေါင်းစပ်ထားသည်။ ဤအရာကို C Programming တွင် **struct** (ဖွဲ့စည်းပုံ) အဖြစ် ဖန်တီးရမည်။

ကျွန်ုပ်တို့၏ Singly Linked List အတွက် Node ဖွဲ့စည်းပုံကို အောက်ပါအတိုင်း သတ်မှတ်နိုင်သည်-

```c
struct Node {
    int data;             // Data ကို သိမ်းဆည်းမည့် နေရာ
    struct Node *next;   // နောက်ဆက်တွဲ Node သို့ ညွှန်ပြသည့် Pointer (Self-referential)
};
```

ဤ `struct Node` သည် **self-referential struct** (ကိုယ်တိုင်ကို ညွှန်ပြသော struct) အယူအဆကို အခြေခံသည်။ ဆိုလိုသည်မှာ `struct Node` တစ်ခုသည် မိမိကိုယ်တိုင်၏ အစိတ်အပိုင်းတစ်ခုအဖြစ် `struct Node *next` ဟု အမည်ပေးထားသည်။ ဤ `next` pointer သည် ထို Node မှ နောက်ထပ် Node တစ်ခု၏ Memory Address ကို သိမ်းဆည်းထားသည်။ ဤ Pointer သည် Linked List ၏ အဓိက အစိတ်အပိုင်းဖြစ်ပြီး Data များအား အစဉ်လိုက် ချိတ်ဆက်ပေးသည်။

### Singly Linked List ၏ အခြေခံအချက်များ

Singly Linked List ကို စီမံခန့်ခွဲရန်အတွက် အဓိကကျသော အချက်အလက်များမှာ List ကို စတင်ရန်နှင့် အဆုံးသတ်ရန်အတွက် **Head Pointer** (ဦးခေါင်း ညွှန်ပြချက်) နှင့် လိုအပ်ပါက **Tail Pointer** (အမြီး ညွှန်ပြချက်) တို့ကို ထိန်းသိမ်းထားရန် လိုအပ်သည်။ Head Pointer သည် List ၏ ပထမဆုံး Node ၏ Address ကို သိမ်းဆည်းထားပြီး၊ ထိုမှစ၍ List တစ်ခုလုံးကို စတင်ကြည့်ရှုနိုင်သည်။

#### Node များ ထည့်သွင်းခြင်း (Insertion)

Node များ ထည့်သွင်းခြင်းသည် Linked List ၏ အဓိက လုပ်ဆောင်ချက်များထဲမှ တစ်ခုဖြစ်သည်။ ထည့်သွင်းပုံအပေါ် မူတည်၍ လုပ်ဆောင်ပုံ ကွဲပြားသည်။

၁။ **Head တွင် ထည့်ခြင်း (Insertion at Head)**:
အသစ်ထည့်မည့် Node ကို List ၏ အစ (Head) တွင် ထည့်ခြင်းဖြစ်သည်။ ဤနည်းလမ်းသည် အလွန်လျင်မြန်သည်။ အသစ်ထည့်မည့် Node ၏ `next` pointer ကို လက်ရှိ Head ၏ Address သို့ ညွှန်ပြစေပြီး၊ ထို့နောက် List ၏ Head ကို အသစ်ထည့်သော Node ၏ Address သို့ ပြောင်းလဲပေးရမည်။

၂။ **Tail တွင် ထည့်ခြင်း (Insertion at Tail)**:
အသစ်ထည့်မည့် Node ကို List ၏ အဆုံး (Tail) တွင် ထည့်ခြင်းဖြစ်သည်။ ဤနည်းလမ်းကို အသုံးချရန်အတွက် Tail Pointer ကို သိထားရန် လိုအပ်သည်။ Tail Node ၏ `next` pointer ကို အသစ်ထည့်မည့် Node ၏ Address သို့ ညွှန်ပြပြီး၊ အသစ်ထည့်မည့် Node ၏ `next` pointer ကို `NULL` သို့ သတ်မှတ်ပေးရမည်။ ထို့နောက် Tail Pointer ကို အသစ်ထည့်သော Node သို့ ပြောင်းလဲပေးရမည်။

၃။ **အလယ်တွင် ထည့်ခြင်း (Insertion in Middle)**:
အလယ်တွင် ထည့်ခြင်းသည် အရှည်သော List များတွင် အသုံးဝင်သည်။ အလယ်တွင် ထည့်ရန်အတွက်၊ ထည့်မည့်နေရာ၏ ရှေ့ရှိ Node (Previous Node) နှင့် နောက်ရှိ Node (Next Node) တို့ကို သိရှိရန် လိုအပ်သည်။ ဥပမာအားဖြင့်၊ အလယ်တွင် ထည့်ရန်အတွက်၊ ထည့်မည့် Node မှ **Previous Node** ၏ `next` pointer ကို **Next Node** သို့ ညွှန်ပြစေပြီး၊ **Next Node** ၏ `next` pointer ကို ထည့်မည့် Node သို့ ညွှန်ပြစေရမည်။ ဤနည်းလမ်းတွင် အလယ်မှ Node တစ်ခုကို ရှာဖွေရန် အချိန်ယူရသဖြင့် $O(n)$ အချိန်ယူရသည်။

#### Node များ ဖယ်ရှားခြင်း (Deletion)

Node တစ်ခုကို ဖယ်ရှားခြင်းသည်လည်း အရေးကြီးသော လုပ်ဆောင်ချက်ဖြစ်သည်။ ဖယ်ရှားမည့် Node ၏ Address ကို သိရှိပြီး၊ ထို Node မှ နောက်ဆက်တွဲ Node သို့ တိုက်ရိုက်ချိတ်ဆက်ပေးရမည်။

၁။ **Head Node ဖယ်ရှားခြင်း (Deletion of Head Node)**:
List ၏ ပထမဆုံး Node ကို ဖယ်ရှားခြင်းဖြစ်သည်။ ဤလုပ်ဆောင်ချက်သည် အလွန်ရိုးရှင်းသည်။ Head Pointer ကို နောက် Node ၏ Address သို့ ပြောင်းလဲပေးရမည်။ ထို့နောက် ဖယ်ရှားမည့် Node ၏ Memory ကို `free()` လုပ်ရမည်။

၂။ **Tail Node ဖယ်ရှားခြင်း (Deletion of Tail Node)**:
List ၏ နောက်ဆုံး Node ကို ဖယ်ရှားခြင်း။ Tail Node ၏ ရှေ့ရှိ Node ၏ `next` pointer ကို `NULL` သို့ ပြောင်းလဲပေးရမည်။ ထို့နောက် Tail Node ၏ Memory ကို `free()` လုပ်ရမည်။

၃။ **အလယ် Node ဖယ်ရှားခြင်း (Deletion of Middle Node)**:
အလယ်ရှိ Node တစ်ခုကို ဖယ်ရှားခြင်း။ ဤလုပ်ဆောင်ချက်တွင် ထို Node ၏ ရှေ့ရှိ Node (Previous Node) ၏ `next` pointer ကို ထို Node ၏ နောက်ဆက်တွဲ Node (Next Node) သို့ တိုက်ရိုက်ချိတ်ဆက်ပေးရမည်။ ထို့နောက် ဖယ်ရှားမည့် Node ၏ Memory ကို `free()` လုပ်ရမည်။ ဤနည်းလမ်းတွင် Node ကို ရှာဖွေရန် အချိန်ယူရသည်။

#### Traversal (အချက်အလက်များ ထုတ်ယူခြင်း)

List တစ်ခုလုံးရှိ Data များအားလုံးကို စတင်မှ အဆုံးထိ လှည့်ပတ်ကြည့်ရှုခြင်းကို **Traversal** (လှည့်ပတ်ကြည့်ရှုခြင်း) ဟု ခေါ်သည်။ ဤလုပ်ဆောင်ချက်အတွက်၊ List ၏ Head Pointer မှ စတင်၍၊ လက်ရှိ Node ၏ `next` pointer ကို အသုံးပြု၍ နောက် Node သို့ ဆက်လက်သွားရမည်။ ဤလုပ်ငန်းစဉ်သည် List ရှိ Data အားလုံးကို တစ်ခုချင်းစီ ထုတ်ယူရန်အတွက် အရေးကြီးသည်။

## ၃။ Doubly Linked List နှင့် Circular Linked List

Singly Linked List သည် တစ်လမ်းသွားသာ ချိတ်ဆက်ထားသောကြောင့် အချက်အလက်များကို နောက်သို့ ပြန်သွား၍ မရပါ။ ထို့ကြောင့် ပိုမိုပြည့်စုံသော Data စီမံခန့်ခွဲမှုအတွက် Doubly Linked List နှင့် Circular Linked List တို့ကို မိတ်ဆက်ပေးလိုသည်။

### Doubly Linked List (နှစ်လမ်းသွား ချိတ်ဆက်ထားသော စာရင်း)

Doubly Linked List သည် Singly Linked List ၏ အားသာချက်ကို ထိန်းသိမ်းထားပြီး နောက်ထပ် အားသာချက်တစ်ခုကို ထပ်ပေါင်းပေးသည်။ ၎င်းသည် Data များကို ရှေ့သို့ (Forward) နှင့် နောက်သို့ (Backward) နှစ်လမ်းသွားစလုံးမှ Navigation လုပ်နိုင်စေသည်။

Node တစ်ခုတွင် Data အပြင် Pointer နှစ်ခုကို ထည့်သွင်းရမည်- တစ်ခုမှာ နောက် Node ကို ညွှန်ပြသော **Next** Pointer နှင့် နောက်တစ်ခုမှာ ရှေ့ Node ကို ညွှန်ပြသော **Previous** Pointer တို့ ဖြစ်သည်။

Node ဖွဲ့စည်းပုံမှာ အောက်ပါအတိုင်း ဖြစ်သည်။

```c
struct DNode {
    int data;
    struct DNode *next;   // ရှေ့သို့ (Forward) ညွှန်ပြချက်
    struct DNode *prev;   // နောက်သို့ (Backward) ညွှန်ပြချက်
};
```

Doubly Linked List တွင် Insertion (ထည့်သွင်းခြင်း) နှင့် Deletion (ဖယ်ရှားခြင်း) များ ပြုလုပ်သည့်အခါ၊ ထည့်မည့်နေရာ၏ ရှေ့ရှိ Node နှင့် နောက်ရှိ Node နှစ်ခုလုံး၏ `next` နှင့် `prev` Pointer များကို မှန်ကန်စွာ ပြန်လည်ပြင်ဆင်ပေးရမည်။ ဥပမာအားဖြင့်၊ Node တစ်ခုကို ထည့်သွင်းသည့်အခါ၊ ထို Node ၏ `next` နှင့် `prev` Pointer များကို အသစ်ထည့်မည့် Node နှင့် ရှိပြီးသား Node များအကြားတွင် ပြန်လည်ချိတ်ဆက်ပေးရမည်။ ဤနည်းလမ်းသည် Singly Linked List ထက် ရှုပ်ထွေးသော်လည်း၊ Data များကို မည်သည့်ဘက်မှမဆို လွယ်ကူစွာ လှည့်ပတ်ကြည့်ရှုနိုင်စေသည်။

### Circular Linked List (စက်ဝိုင်းပုံ ချိတ်ဆက်ထားသော စာရင်း)

Circular Linked List သည် Linked List ၏ အထူးပုံစံတစ်ခုဖြစ်သည်။ ၎င်း၏ ထူးခြားချက်မှာ List ၏ နောက်ဆုံး Node (Tail Node) သည် နောက်ထပ် Node အဖြစ် List ၏ ပထမဆုံး Node (Head Node) သို့ ပြန်လည်ညွှန်ပြခြင်း (Self-loop) ဖြစ်သည်။ ဆိုလိုသည်မှာ List ၏ အဆုံးတွင် `NULL` မရှိဘဲ၊ နောက်ဆုံး Node ၏ `next` Pointer သည် Head Node ကို ညွှန်ပြနေသည်။

Circular List တွင် Navigation လုပ်ရာ၌၊ List ၏ အဆုံးသို့ရောက်သောအခါ ထပ်မံ၍ နောက်တစ်ခုသို့ ဆက်သွားမည့်အစား၊ ပြန်၍ List ၏ အစသို့ ပြန်ရောက်သွားသည်။ ဤအယူအဆသည် List ကို စက်ဝိုင်းပုံ (Circle) ပုံစံအဖြစ် ဖော်ပြသည်။

Circular Linked List တွင် Insertion နှင့် Deletion များ ပြုလုပ်သည့်အခါ၊ ဤ Self-loop အချက်ကို ထိန်းသိမ်းရန် အထူးဂရုစိုက်ရမည်။ Insertion ပြုလုပ်သည့်အခါ၊ Node တစ်ခုကို ထည့်သွင်းသည့်အခါ၊ ၎င်း၏ `next` Pointer သည် List ၏ စက်ဝိုင်းပုံ ပုံစံကို ထိန်းသိမ်းထားရန် အရေးကြီးသည်။ ဥပမာအားဖြင့်၊ List တွင် အလယ်မှ Node တစ်ခုကို ဖယ်ရှားသည့်အခါ၊ ထို Node ၏ ရှေ့ရှိ Node ၏ `next` Pointer နှင့် နောက်ရှိ Node ၏ `prev` Pointer တို့ကို ပြန်လည်ချိတ်ဆက်ပေးရမည်။

## ၄။ Array နှင့် Linked List နှိုင်းယှဉ်ခြင်း (Trade-offs Analysis)

Array နှင့် Linked List တို့သည် Data များကို သိမ်းဆည်းသည့် မတူညီသော နည်းလမ်းများ ဖြစ်ကြသည်။ ၎င်းတို့၏ အကျိုးအမြတ်နှင့် အားနည်းချက်များကို နှိုင်းယှဉ်ကြည့်ခြင်းဖြင့် မည်သည့်အချိန်တွင် မည်သည့် Data Structure ကို အသုံးပြုသင့်သည်ကို ဆုံးဖြတ်နိုင်သည်။

### Space Complexity နှင့် Time Complexity နှိုင်းယှဉ်ချက်

**Space Complexity** (နေရာအသုံးပြုမှု) နှင့် **Time Complexity** (အချိန်အသုံးပြုမှု) တို့ကို နှိုင်းယှဉ်ကြည့်ရအောင်။

**Array များ** တွင် Data များသည် Memory တွင် တစ်ဆက်တည်း သိမ်းဆည်းထားသောကြောင့် အလွန်ထိရောက်သည်။ Data တစ်ခုကို ဝင်ရောက်ကြည့်ရှုရန် (Access) အလွန်လျင်မြန်သည်။ Array တွင် Data တစ်ခုကို သိမ်းဆည်းရန်အတွက်သာ လိုအပ်သော နေရာကိုသာ အသုံးပြုသည်။ သို့သော် Insertion နှင့် Deletion များပြုလုပ်သည့်အခါ၊ အလယ်မှ Data များအားလုံးကို ရွှေ့ပြောင်းရသောကြောင့် Time Complexity သည် $O(n)$ ဖြစ်သည်။

**Linked List များ** တွင် Data များသည် Memory ၏ မည်သည့်နေရာတွင်မဆို လွတ်လပ်စွာ သိမ်းဆည်းထားပြီး Pointer များဖြင့် ချိတ်ဆက်ထားသည်။ Data တစ်ခုကို ဝင်ရောက်ကြည့်ရှုရန် (Access) အစမှစ၍ တစ်ခုချင်းစီ လိုက်ကြည့်ရသောကြောင့် Time Complexity သည် $O(n)$ ဖြစ်သည်။ သို့သော်၊ အသစ်ထည့်ခြင်း (Insertion) သို့မဟုတ် ဖယ်ရှားခြင်း (Deletion) များပြုလုပ်သည့်အခါ၊ ထိုနေရာသို့ ရောက်ရှိရန်အတွက် Pointer များအား ပြင်ဆင်ရုံသာ ဖြစ်သောကြောင့် အချိန်သည် $O(1)$ (Position ကို သိလျှင်) ဖြစ်သည်။

### ဘယ်အချိန်မှာ ဘယ်ဟာ သုံးသင့်သလဲ (Use Cases)

**Array များ** ကို အသုံးပြုသင့်သည့် အခြေအနေများမှာ Data များ၏ အရေအတွက် **အမြဲတမ်း သိထားပြီး**၊ Data များအား အလွန်လျင်မြန်စွာ **Access** လုပ်ရန် လိုအပ်သောအခါများ ဖြစ်သည်။ ဥပမာအားဖြင့်၊ ဂိမ်းများတွင် ကစားသမားများ၏ စွမ်းဆောင်ရည်အချက်အလက်များ၊ သို့မဟုတ် အချိန်တိုင်းအတွက် တည်ငြိမ်စွာ သိမ်းဆည်းထားရမည့် ကိန်းဂဏန်းများအတွက် Array များသည် အကောင်းဆုံးဖြစ်သည်။

**Linked List များ** ကို အသုံးပြုသင့်သည့် အခြေအနေများမှာ Data များ၏ အရေအတွက် **မသေချာသောအခါ** (Dynamic Size) သို့မဟုတ် Data များအား **မကြာခဏ Insertion နှင့် Deletion** လုပ်ရသောအခါများ ဖြစ်သည်။ ဥပမာအားဖြင့်၊ စာရင်းများ (Lists)၊ အဖြစ်အပျက်များ၏ စီးဆင်းမှုများ (Event Streams) သို့မဟုတ် Data များ အမြဲတမ်း ဝင်လာနိုင်သော စနစ်များတွင် Linked List များသည် Array များထက် ပိုမိုထိရောက်သည်။

### Trade-off များ (Trade-offs)

Array နှင့် Linked List တို့ကြားရှိ အဓိက Trade-off များမှာ Memory Access နှင့် Pointer Management တို့တွင် ရှိသည်။

**Memory Access:** Array များသည် Contiguous Memory တွင် ရှိသောကြောင့် CPU သည် Memory Address ကို သိရှိရုံဖြင့် Data ကို အလွန်လျင်မြန်စွာ ဖတ်ရှုနိုင်သည်။ Linked List များသည် Memory တွင် တစ်နေရာတည်း မဟုတ်ဘဲ ပျံ့နှံ့နေသောကြောင့် Pointer များမှတစ်ဆင့် တစ်ခုချင်းစီကို လိုက်ကြည့်ရသောကြောင့် Memory Access သည် Array များထက် နှေးကွေးနိုင်သည်။

**Pointer Management:** Array များတွင် Pointer များ မလိုအပ်ဘဲ Index ကို အသုံးပြုရသည်။ Linked List များတွင် Data များအား ချိတ်ဆက်ထားသည့် Pointer များ (Next/Previous) ကို ကိုယ်တိုင် စီမံခန့်ခွဲရသည်။ ဤ Pointer များ မှန်ကန်စွာ ထိန်းသိမ်းရန် အလွန်အရေးကြီးပြီး၊ မှားယွင်းစွာ စီမံခန့်ခွဲပါက **Dangling Pointer** (လိပ်စာ မှားယွင်းသော ညွှန်ပြချက်) သို့မဟုတ် **Memory Leak** (အသုံးမပြုတော့သော Memory ကို လွှတ်မပေးခြင်း) များ ဖြစ်ပေါ်လာနိုင်သည်။

## ၅။ လက်တွေ့ အကောင်အထည်ဖော်ခြင်း (Practical Implementation)

အခြေခံအယူအဆများကို နားလည်ပြီးနောက်၊ Singly Linked List ကို C Programming ဖြင့် လက်တွေ့ အကောင်အထည်ဖော်ခြင်းသည် အရေးကြီးဆုံး သင်ခန်းစာဖြစ်သည်။ ဤအဆင့်တွင် ကျွန်ုပ်တို့သည် Dynamic Memory Allocation နှင့် Pointer များကို အသုံးပြုပုံကို နားလည်ရမည်။

### Singly Linked List ကို C ဖြင့် အပြည့်အဝ Implement လုပ်ခြင်း

ကျွန်ုပ်တို့သည် Singly Linked List ကို အသုံးပြု၍ Data များ ထည့်သွင်းခြင်း (Insertion)၊ ဖယ်ရှားခြင်း (Deletion) နှင့် လှည့်ပတ်ကြည့်ရှုခြင်း (Traversal) တို့ကို လုပ်ဆောင်မည့် Code ကို ရေးသားမည်။

ပထမဆုံးအနေဖြင့် Node ဖွဲ့စည်းပုံနှင့် List Pointer များအတွက် `struct` များအား `typedef` ဖြင့် သတ်မှတ်ရမည်။ ဤသည်မှာ ကျွန်ုပ်တို့၏ Data structure ကို စနစ်တကျ ဖော်ပြပေးသည်။

```c
#include <stdio.h>
#include <stdlib.h> // For malloc and free

// Define the structure for a Node
struct Node {
    int data;             // The data to be stored in the node
    struct Node *next;    // Pointer to the next node
};

// Define the type for a pointer to a Node
typedef struct Node *NodePtr;

// Global pointer to the head of the list
NodePtr head = NULL;
```

List ကို စတင်ရန်နှင့် Memory Allocation ပြုလုပ်ရန် လိုအပ်သည်။ Linked List သည် Dynamic ဖြစ်သောကြောင့် `malloc` (Memory Allocation) ကို အသုံးပြု၍ Heap Memory တွင် Node များကို တိုးတက်တက်ထပ်ထပ် ဖန်တီးရမည်။

**List ကို စတင်ခြင်းနှင့် Memory Allocation:**
List တစ်ခုကို စတင်ရန်အတွက် `head` pointer ကို `NULL` သို့ သတ်မှတ်ထားရမည်။ အသစ်ထည့်မည့် Node တစ်ခုကို ဖန်တီးရန်အတွက် `malloc` function ကို အသုံးပြုရမည်။

```c
// Function to create a new node
struct Node* createNode(int value) {
    // Allocate memory for the new node
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    
    if (newNode == NULL) {
        printf("Memory allocation failed!\n");
        exit(1); // Exit if memory allocation fails
    }
    
    // Initialize the data and set next to NULL
    newNode->data = value;
    newNode->next = NULL;
    
    return newNode;
}
```

**အဓိက လုပ်ဆောင်ချက်များ (CRUD Operations) ကို Code ဖြင့် ပြသခြင်း:**

**၁။ Insertion (အလယ်နှင့် အစ)**

*   **Head တွင် ထည့်ခြင်း (Insertion at Head):**
    အသစ်ထည့်မည့် Node ကို List ၏ အစတွင် ထည့်ခြင်း။

```c
void insertAtHead(int value) {
    struct Node* newNode = createNode(value);
    
    // If the list is empty, the new node becomes the head
    if (head == NULL) {
        head = newNode;
        printf("%d inserted at the head.\n", value);
        return;
    }
    
    // If the list is not empty, update head and point new node to old head
    newNode->next = head;
    head = newNode;
    printf("%d inserted at the head.\n", value);
}
```

*   **အလယ်တွင် ထည့်ခြင်း (Insertion in Middle):**
    အလယ်တွင် ထည့်ရန်အတွက်၊ ကျွန်ုပ်တို့သည် List ၏ အရှေ့မှ Node ကို ရှာဖွေရမည်။ ဤနေရာတွင် အလယ်မှ Node ကို ရှာဖွေရန်အတွက် `O(n)` အချိန်ယူရမည်။

```c
void insertInMiddle(int value, int prev_index) {
    // For simplicity, we will assume prev_index is the index of the node BEFORE which we insert.
    // In a real scenario, we need to traverse to find the correct position.
    if (prev_index < 0 || prev_index >= (int)(head ? (int)(head - head->next) : 0)) {
        printf("Invalid index for insertion.\n");
        return;
    }
    
    struct Node* newNode = createNode(value);
    struct Node* current = head;
    int count = 0;
    
    // Traverse to the node before the insertion point
    while (current != NULL && count < prev_index) {
        current = current->next;
        count++;
    }
    
    // Check if the position is valid (we need the node *before* the insertion point)
    if (current == NULL) {
        printf("Insertion failed: Invalid position.\n");
        free(newNode);
        return;
    }
    
    // Perform the insertion
    newNode->next = current->next;
    current->next = newNode;
    printf("%d inserted at position %d.\n", value, prev_index + 1);
}
```

**၂။ Deletion (အလယ်နှင့် အဆုံး)**

*   **Head Node ဖယ်ရှားခြင်း (Deletion of Head Node):**
    List ၏ ပထမဆုံး Node ကို ဖယ်ရှားခြင်း။

```c
void deleteHead() {
    if (head == NULL) {
        printf("List is empty. Cannot delete head.\n");
        return;
    }
    
    struct Node* temp = head;
    head = head->next; // Move head to the next node
    
    printf("%d deleted from the head.\n", temp->data);
    free(temp); // Free the memory of the old head
}
```

*   **Tail Node ဖယ်ရှားခြင်း (Deletion of Tail Node):**
    List ၏ နောက်ဆုံး Node ကို ဖယ်ရှားခြင်း။

```c
void deleteTail() {
    if (head == NULL) {
        printf("List is empty. Cannot delete tail.\n");
        return;
    }
    
    struct Node* current = head;
    // Traverse to the last node
    while (current->next != NULL) {
        current = current->next;
    }
    
    // If the list has only one node
    if (current->next == head) {
        head = NULL;
        free(current);
        printf("%d deleted from the tail (only node).\n", current->data);
        return;
    }
    
    // If there is more than one node
    struct Node* temp = current;
    current->next = NULL; // The new tail points to NULL
    free(temp);
    printf("%d deleted from the tail.\n", temp->data);
}
```

**၃။ Traversal (အချက်အလက်များ ထုတ်ယူခြင်း)**

List တစ်ခုလုံးရှိ Data များအားလုံးကို စတင်မှ အဆုံးထိ လှည့်ပတ်ကြည့်ရှုခြင်း။

```c
void traverseList() {
    struct Node* current = head;
    printf("\nList elements (Traversal):\n");
    if (current == NULL) {
        printf("List is empty.\n");
        return;
    }
    while (current != NULL) {
        printf("%d -> ", current->data);
        current = current->next;
    }
    printf("NULL\n");
}
```

### Debugging နှင့် Memory Management

Linked List များတွင် Pointer များဖြင့် အလုပ်လုပ်သောကြောင့် Memory Management သည် အလွန်အရေးကြီးသည်။

**NULL Pointer နှင့် Dangling Pointer များ:**
`malloc` ဖြင့် Memory ကို ခွဲဝေပေးပြီး `free()` ဖြင့် လွှတ်ပေးရသည်။ `free()` လုပ်ပြီးနောက် ထို Pointer ကို မသုံးတော့ဘဲ ထပ်မံအသုံးပြုပါက ထို Pointer သည် **Dangling Pointer** (လိပ်စာ မှားယွင်းသော ညွှန်ပြချက်) ဖြစ်သွားပြီး၊ ထိုလိပ်စာကို ပြန်လည်အသုံးပြုရန် ကြိုးစားသည့်အခါ **Segmentation Fault** (စနစ်ပိုင်းဆိုင်ရာ အမှား) များ ဖြစ်ပေါ်စေနိုင်သည်။ ထို့ကြောင့် `free()` လုပ်ပြီးနောက် ထို Pointer များကို `NULL` သို့ သတ်မှတ်ပေးရန် အလေ့အထရှိသည်။

**`malloc` နှင့် `free` ကို မှန်ကန်စွာ အသုံးပြုခြင်းနှင့် `memory leak` ရှောင်ရှားနည်းများ:**
`malloc()` ဖြင့် Memory ကို ခွဲဝေပေးပြီး `free()` ဖြင့် လွှတ်ပေးခြင်းသည် Memory Leak ကို ရှောင်ရှားရန် အခြေခံဖြစ်သည်။ `free()` ကို မှန်ကန်စွာ အသုံးပြုခြင်းဖြင့် လိုအပ်သော Memory ကို ပြန်လည်ရရှိစေသည်။ Memory Leak ဆိုသည်မှာ `malloc` လုပ်ပြီးသော Memory ကို `free` မလုပ်ဘဲ ပရိုဂရမ် အဆုံးသတ်သွားခြင်း သို့မဟုတ် အခြားနေရာတွင် အသုံးမပြုတော့ဘဲ ထားခြင်းကြောင့် ဖြစ်ပေါ်လာသည်။

**`Valgrind` ကဲ့သို့သော Tool များကို အသုံးပြုခြင်း:**
Code ၏ မှန်ကန်မှုကို စစ်ဆေးရန်အတွက် **Valgrind** ကဲ့သို့သော Debugging Tool များကို အသုံးပြုသင့်သည်။ ဤ Tool များသည် Memory Access Errors (ဥပမာ: Invalid Read/Write) များ၊ Memory Leaks များကို ရှာဖွေပေးနိုင်သည်။ Linked List ကဲ့သို့သော Pointer-based Data Structure များတွင် ဤ Tools များသည် အလွန်အသုံးဝင်သည်။

## ၆။ နိဂုံးချုပ် (Conclusion)

ဤအခန်းတွင် ကျွန်ုပ်တို့သည် Array များ၏ ကန့်သတ်ချက်များကို ကျော်လွှားပြီး Dynamic Data Structure တစ်ခုဖြစ်သော Linked List ၏ အခြေခံများကို လေ့လာခဲ့ကြသည်။ Linked List သည် Data များကို Node များအဖြစ် ခွဲခြားပြီး Pointer များဖြင့် ချိတ်ဆက်ထားခြင်းဖြင့် Data များ ထည့်သွင်းခြင်းနှင့် ဖယ်ရှားခြင်းတို့ကို Array များထက် ပိုမိုထိရောက်သော $O(1)$ အချိန်ဖြင့် လုပ်ဆောင်နိုင်စေသည်။ Doubly Linked List နှင့် Circular Linked List များကဲ့သို့သော ပိုမိုရှုပ်ထွေးသော ပုံစံများကိုလည်း နားလည်လာခဲ့သည်။

Array သည် အလွယ်တကူ Access လုပ်ရန်နှင့် Data များ အမြဲတမ်း သိထားရန် လိုအပ်သည့်အခါတွင် အကောင်းဆုံးဖြစ်ပြီး၊ Linked List သည် Data များ၏ အရေအတွက် မသေချာသောအခါနှင့် မကြာခဏ ပြောင်းလဲနေသော အခြေအနေများတွင် ပိုမိုသင့်လျော်သည်။ ဤ Trade-off များသည် Memory Access နှင့် Pointer Management တို့၏ အကျိုးအပြစ်များကြောင့် ဖြစ်ပေါ်လာသည်။

ကျွန်ုပ်တို့သည် Singly Linked List ကို C Programming ဖြင့် လက်တွေ့ Implement လုပ်ခြင်းဖြင့် Dynamic Data Structure များ၏ အခြေခံကျသော နည်းပညာများကို လက်တွေ့အသုံးချနိုင်ခဲ့ပြီ ဖြစ်သည်။ Linked List သည် Data Structure များ၏ အခြေခံအုတ်မြစ်တစ်ခုဖြစ်ပြီး၊ Stack, Queue, Tree စသည့် Data Structure များ၏ အခြားအမျိုးအစားများကို လေ့လာရန်အတွက် အကောင်းဆုံး အခြေခံအမှတ်အသား ဖြစ်သည်။ နောက်အခန်းများတွင် Stack, Queue, Tree စသည့် Data Structure များအကြောင်းကို ဆက်လက်လေ့လာသွားမည် ဖြစ်သည်။