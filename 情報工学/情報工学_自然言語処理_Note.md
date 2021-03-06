# 自然言語処理 [NLP : natural language processing]

自然言語処理（NLP）に関してのマイノートです。<br>
特に、ニューラルネットワーク、ディープラーニングによる自然言語処理（NLP）を重点的に取り扱っています。<br>
今後も随時追加予定です。<br>

![default](https://user-images.githubusercontent.com/25688193/34451758-bdae080a-ed73-11e7-84f3-b649dcf534d9.jpg)

尚、ニューラルネットワークに関しては、以下の記事に記載しています。

- [星の本棚（ニューラルネットワーク）](http://yagami12.hatenablog.com/entry/2017/09/17/111935#ID_10-4-3)

又、より一般的な機械学習に関しては、以下の記事に記載しています。

- [星の本棚（機械学習）](http://yagami12.hatenablog.com/entry/2017/09/17/111400)

## 目次 [Contents]
1. [自然言語処理（NLP）](#ID_10)
    1. one-hot encode と one-hot ベクトル    
    1. [埋め込みベクトル [embedding vector] と埋め込み行列 [embedding matrix]](#ID_10-2)
    1. [言語モデル [LM : Language model]](#ID_10-3)
        1. N グラム言語モデル
        1. [ニューラル言語モデル [NLM : Neural Language Model]](#ID_10-3-2)
            1. [順伝播型ニューラル言語モデル（FFNN-LM）](#ID_10-3-2-1)
            1. [再帰ニューラル（RNN）言語モデル [RNN-LM]](#ID_10-3-2-2)
        1. 言語モデルの評価
            1. パープレキシティ [PPL : Perplexity]
    1. 形態素解析 [Morphological Analysis]
    1. [分散表現 [distributional / distributed]](#ID_10-4)
        1. [単語の分散表現、単語埋め込み [Word Embeddings]](#ID_10-4-1)
        1. [単語の分散表現、単語埋め込み [Word Embeddings] の具体的な獲得方法](#ID_10-4-2)
            1. [ニューラル言語モデルを用いた分散表現の獲得方法](#ID_10-4-2-1)
            1. [対数双線形モデルを用いた分散表現の獲得方法](#ID_10-4-2-2)
        1. [word2vec ツール](#ID_10-4-3)
            1. [CBOW [Countinuous Bag-of-Words] モデル](#ID_10-4-3-1)
            1. [skip-gram モデル](#ID_10-4-3-2)
            1. [負例サンプリング [Negative Sampling] による skip-gram モデルの学習の高速化](#ID_10-4-3-3)
            1. 階層的ソフトマックス [HSM : hierarchical softmax] による skip-gram モデルの学習の高速化
    1. [系列変換モデル [sequence-to-sequence / seq2seq]](#ID_10-5)
        1. [モデルの構造（アーキテクチャ）[model architecture]](#ID_10-5-1)
            1. [符号化器 - 埋め込み層 [encoder embedding layer]](#ID_10-5-1-1)
            1. [符号化器 - 再帰層 [encoder recurrent layer]](#ID_10-5-1-2)
            1. [復号化器 - 埋め込み層 [decoder embedding layer]](#ID_10-5-1-3)
            1. [復号化器 - 再帰層 [decoder recurrent layer]](#ID_10-5-1-4)
            1. [復号化器 - 出力層 [decoder output layer]](#ID_10-5-1-5)
            1. [seq2seq モデルの処理負荷](#ID_10-5-1-6)
        1. [seq2seq モデルの学習方法](#ID_10-5-2)
        1. [seq2seq モデルにおける系列生成方法](#ID_10-5-3)
            1. [貪欲法 [greedy algorithm]](#ID_10-5-3-1)
            1. [ビーム探索 [beam search]](#ID_10-5-3-2)
    1. [注意機構 [attention mechanism] / seq2seq model](#ID_10-6)
        1. [ソフト注意機構 [soft attention mechanism]](#ID_10-6-1)
            1. [seq2seq モデルでのソフト注意機構 [soft attention mechanism]](#ID_10-6-1-1)
            1. [より一般的なモデルでのソフト注意機構 [soft attention mechanism]](#ID_10-6-1-2)
        1. [ハード注意機構 [hard attention mechanism]](#ID_10-6-2)
    1. [記憶ネットワーク [MemN : memory networks]](#ID_10-7)
        1. [記憶ネットワークのアーキテクチャ [architecture]](#ID_10-7-0)
        1. [教師あり記憶ネットワーク [supervised memory networks / strongly supervised memory networks]](#ID_10-7-1)
            1. [I : 入力情報変換 [input feature map]](#ID_10-7-1-1)
            1. [G : 一般化 [genelarization]](#ID_10-7-1-2)
            1. [O : 出力情報変換 [output feature map]](#ID_10-7-1-3)
        1. [end-to-end 記憶ネットワーク [end-to-end memory networks]](#ID_10-7-2)
            1. [I : 入力情報変換 [input feature map]](#ID_10-7-2-1)
            1. [G : 一般化 [genelarization]](#ID_10-7-2-2)
            1. [O : 出力情報変換 [output feature map]](#ID_10-7-2-3)
        1. [動的記憶ネットワーク [DMN : dynamic memory networks]](#ID_10-7-3)
    1. [ニューラル言語モデル、seq2seq モデルの出力層の高速化手法（クロス・エントロピー損失関数の勾配計算の効率化）](#ID_10-8)
        1. [重点サンプリング [importance sampling]](#ID_10-8-1)
        1. [雑音対照推定 [NCE : noise-contrastive estimation]](#ID_10-8-2)
        1. [負例サンプリング [negative sampling]](#ID_10-8-3)
        1. [ブラックアウト [black-out]](#ID_10-8-4)
        1. [階層的ソフトマックス [HSM : hierarchial softmax]](#ID_10-8-5)
        1. [各種高速化手法の比較](#ID_10-8-6)
    1. [自然言語処理の応用タスク [application]](#ID_10-9)
        1. [機械翻訳 [MT : machine translation]](#ID_10-9-1)
            1. ニューラル翻訳 [NMT : neural machine translation] / ニューラル翻訳モデル
            1. [GroundHog / RNNSearch](#ID_10-9-1-1)
            1. [OpenNMT / seq2seq-attn](#ID_10-9-1-2)
                1. [符号化器 [Encoder] / 2 層の Bidirectional-LSTM](#ID_10-9-1-2-1)
                1. [復号化器 [Decoder] / 2 層の LSTM + attention 層](#ID_10-9-1-2-2)
            1. [機械翻訳タスクで共通の課題とその対策、改良](#ID_10-9-1-3)
                1. [語彙数、未知語と入出力単位](#ID_10-9-1-3-1)
                1. [過剰生成 [over-generation]、不足生成 [under-generation] と被覆 [coverage]](#ID_10-9-1-3-2)
        1. [文書要約 [text summarization]](#ID_10-9-2)
            1. [見出し生成タスク [headline generation task] / 短文生成タスク](#ID_10-9-2-1)
                1. [文書要約タスクでの Encoder-Decoder 方式 / attention 構造を用いるモデル](#ID_10-9-2-1-1)
                    1. [「A Neural Attention Model for Abstractive Sentence Summarization」/ Attention-Based Summarization (ABS)](#ID_10-9-2-1-1-1)
                1. [RNN による ABS モデルの拡張、改良](#ID_10-9-2-1-2)
                1. その他の改良
        1. [対話システム [dialog system]](#ID_10-9-3)
            1. [対話モデル](#ID_10-9-3-1)
                1. [対話システムにおける seq2seq モデルの適用](#ID_10-9-3-1-1)
                1. [attention 構造を用いた、対話モデル](#ID_10-9-3-1-2)
                1. [対話システムの特徴である話者交代と発話者を積極的にモデルに取り組んだ手法](#ID_10-9-3-1-3)
            1. [対話モデルの発展](#ID_10-9-3-2)
            1. [対話システムの自動評価](#ID_10-9-3-3)
        1. [質問応答 [QA : question answering]](#ID_10-9-4)
            1. [回答選択タスク](#ID_10-9-4-1)
            1. [回答選択問題の評価方法](#ID_10-9-4-2)
            1. [end-to-end な質問応答](#ID_10-9-4-3)
    1. [参考文献](#参考文献)

<a id="ID_10"></a>

## 自然言語処理（NLP）

<a id="ID_10-1"></a>

<!--
### one-hot encode と one-hot ベクトル
> 記載中...
-->

<a id="ID_10-2"></a>

### 埋め込みベクトル [embedding vector] と埋め込み行列 [embedding matrix]
![image](https://user-images.githubusercontent.com/25688193/34094596-26e24d16-e411-11e7-95d3-1971133297c1.png)


<a id="ID_10-3"></a>

### 言語モデル [LM : Language model]
![image](https://user-images.githubusercontent.com/25688193/34341685-05559ffc-e9e0-11e7-8380-3a905352754c.png)
![image](https://user-images.githubusercontent.com/25688193/34341696-37917a36-e9e0-11e7-9281-efb5294dd58a.png)
![image](https://user-images.githubusercontent.com/25688193/34341814-cd99e62e-e9e2-11e7-8de5-a94fe5a6d2d2.png)
![image](https://user-images.githubusercontent.com/25688193/34342794-a5966640-e9fe-11e7-93dc-b9245c1a611e.png)
![image](https://user-images.githubusercontent.com/25688193/34342701-3cbea040-e9fb-11e7-9680-03e146549cc4.png)
![image](https://user-images.githubusercontent.com/25688193/34342734-b8146f80-e9fc-11e7-8fe4-ee99fd46cb87.png)


<a id="ID_10-3-1"></a>

<!--
### N グラム言語モデル
記載中...
-->

<a id="ID_10-3-2"></a>

### ニューラル言語モデル [NNLM : Neural network Language model ]

<a id="ID_10-3-2-1"></a>

#### 順伝播型ニューラル言語モデル（FFNN-LM）
![image](https://user-images.githubusercontent.com/25688193/34349562-19147962-ea55-11e7-9487-96780bed2a74.png)
![image](https://user-images.githubusercontent.com/25688193/34351744-e686df00-ea61-11e7-85dd-d32f73e1d589.png)
![image](https://user-images.githubusercontent.com/25688193/34355192-d80a567c-ea76-11e7-83c7-2b68388608dd.png)
![image](https://user-images.githubusercontent.com/25688193/34361963-788001ca-eab2-11e7-8985-1c24d2b1beb3.png)


<a id="ID_10-3-2-2"></a>

#### 再帰ニューラル言語モデル（RNN-LM）
![image](https://user-images.githubusercontent.com/25688193/34355245-34a868c4-ea77-11e7-95a4-4bf84dd09ae6.png)
![image](https://user-images.githubusercontent.com/25688193/34359181-1bb80866-ea99-11e7-9241-6e346425b392.png)
![image](https://user-images.githubusercontent.com/25688193/34355272-62e4239a-ea77-11e7-9ae0-62210d7509fc.png)
![image](https://user-images.githubusercontent.com/25688193/34362048-60889040-eab3-11e7-9996-f639a6bf5ead.png)


<a id="ID_10-4"></a>

### 分散表現 [distributional / distributed]
![image](https://user-images.githubusercontent.com/25688193/34366909-eee0f68e-eae5-11e7-8fe8-bd36d46f00f1.png)
![image](https://user-images.githubusercontent.com/25688193/34368672-000af334-eaf9-11e7-8425-c5acd7036701.png)
![image](https://user-images.githubusercontent.com/25688193/34368876-c70ae9c0-eafa-11e7-882d-bbf5b65b7352.png)
![image](https://user-images.githubusercontent.com/25688193/34369022-fa7eee86-eafb-11e7-94ae-8be2fe02f0b1.png)


<a id="ID_10-4-1"></a>

#### 単語の分散表現 [disturibute representation]、単語埋め込み [Word Embeddings]
![image](https://user-images.githubusercontent.com/25688193/34368756-ad274428-eaf9-11e7-8bc4-d68876b8027d.png)
![image](https://user-images.githubusercontent.com/25688193/34102231-ad432a1e-e42b-11e7-8aa2-12920b882ebd.png)
![image](https://user-images.githubusercontent.com/25688193/34108443-66e29466-e443-11e7-9145-bc1921e90498.png)

<a id="ID_10-4-2"></a>

#### 単語の分散表現、単語埋め込み [Word Embeddings] の具体的な獲得方法
![image](https://user-images.githubusercontent.com/25688193/34370735-ed89bd24-eb09-11e7-9732-bf39e23985c0.png)

<a id="ID_10-4-2-1"></a>

#### ニューラル言語モデルを用いた分散表現の獲得方法
![image](https://user-images.githubusercontent.com/25688193/34377024-6ab57900-eb32-11e7-993b-4b8a636a6c3c.png)
![image](https://user-images.githubusercontent.com/25688193/34377036-78a46562-eb32-11e7-8420-8c3e8967b3f8.png)
![image](https://user-images.githubusercontent.com/25688193/34377396-31308cfe-eb34-11e7-85b2-4d0cc615ce18.png)


<a id="ID_10-4-2-2"></a>

#### 対数双線形モデルを用いた分散表現の獲得方法
![image](https://user-images.githubusercontent.com/25688193/34452890-9b39ef32-ed8c-11e7-9700-1b596e13584f.png)



<a id="ID_10-4-3"></a>

### word2vec ツール
![image](https://user-images.githubusercontent.com/25688193/34453040-3ad4665c-ed8e-11e7-8a19-1deab212869e.png)

<a id="ID_10-4-3-1"></a>

#### CBOW [Countinuous Bag-of-Words] モデル
![image](https://user-images.githubusercontent.com/25688193/34443731-6cf88154-ed0c-11e7-9b94-75e065a4026d.png)
![image](https://user-images.githubusercontent.com/25688193/34443022-955317d4-ed09-11e7-8c2b-ceb4ebb0669e.png)
![image](https://user-images.githubusercontent.com/25688193/34441364-aaa8d606-ecfe-11e7-9909-34028aabc0ca.png)
![image](https://user-images.githubusercontent.com/25688193/34436963-c1059824-ecdd-11e7-8230-884cfb87113a.png)
![image](https://user-images.githubusercontent.com/25688193/34436979-cf35ab00-ecdd-11e7-9fc6-e1aab309fd57.png)
![image](https://user-images.githubusercontent.com/25688193/34441458-340083b8-ecff-11e7-8034-862f4cb58912.png)

<a id="ID_10-4-3-2"></a>

#### skip-gram モデル
> 記載＆修正中...<br>
![image](https://user-images.githubusercontent.com/25688193/34443558-5b664f62-ed0b-11e7-85c5-95788e8cdd5f.png)
![image](https://user-images.githubusercontent.com/25688193/34444167-88e435c2-ed0f-11e7-82ee-ae6e6c7831f5.png)
![image](https://user-images.githubusercontent.com/25688193/34444399-4782fe36-ed11-11e7-918e-816c2f1ba9cd.png)
![image](https://user-images.githubusercontent.com/25688193/34444193-adb38092-ed0f-11e7-8ccd-c1fd1bbf41b4.png)

- 参考サイト : http://tkengo.github.io/blog/2016/05/09/understand-how-to-learn-word2vec/


<a id="ID_10-4-3-3"></a>

#### 負例サンプリング [Negative Sampling] による skip-gram モデルの学習の高速化
![image](https://user-images.githubusercontent.com/25688193/34534531-d080fe9c-f101-11e7-88bd-ec0926b34f8f.png)
![image](https://user-images.githubusercontent.com/25688193/34535444-20aaeaa6-f105-11e7-92bc-ca7b1a9a1f72.png)
![image](https://user-images.githubusercontent.com/25688193/34535467-380fb4a6-f105-11e7-8bda-4bfc514729d7.png)
![image](https://user-images.githubusercontent.com/25688193/34535495-5f420af6-f105-11e7-8f94-7b3c5ebb7ad1.png)



<a id="ID_10-5"></a>

## 系列変換モデル [sequence-to-sequence / seq2seq]
![image](https://user-images.githubusercontent.com/25688193/34563308-81db5b0e-f195-11e7-947b-64980e17d825.png)
![image](https://user-images.githubusercontent.com/25688193/34565703-3270a68c-f19f-11e7-8e34-f2cb8699889a.png)
![image](https://user-images.githubusercontent.com/25688193/34581706-cd833a88-f1d4-11e7-9ede-6280366ccd99.png)
![image](https://user-images.githubusercontent.com/25688193/34582513-6cc63166-f1d7-11e7-8d2d-9102cf04b73d.png)
![image](https://user-images.githubusercontent.com/25688193/34589628-10d95d7e-f1f5-11e7-98c2-dcd596d79ec7.png)
![image](https://user-images.githubusercontent.com/25688193/34598482-4e2ced40-f230-11e7-8269-b667c1f2f8a7.png)
![image](https://user-images.githubusercontent.com/25688193/34598799-37953afe-f232-11e7-870a-00b5f9846649.png)
![image](https://user-images.githubusercontent.com/25688193/34599033-c56c4790-f233-11e7-8738-39ccdab616d5.png)


<a id="ID_10-5-1"></a>

### モデルの構造（アーキテクチャ）[model architecture]
![image](https://user-images.githubusercontent.com/25688193/34601992-80ab203c-f241-11e7-87b0-7b19d3f54c21.png)
![image](https://user-images.githubusercontent.com/25688193/34602043-b2bf0dd6-f241-11e7-9328-5d8765bdc309.png)

<a id="ID_10-5-1-1"></a>

#### 符号化器 - 埋め込み層 [encoder - embedding layer]
![image](https://user-images.githubusercontent.com/25688193/34607679-0b07fe88-f258-11e7-8b33-61f08f81fd02.png)
![image](https://user-images.githubusercontent.com/25688193/34607696-18257a1e-f258-11e7-9946-52186aae6160.png)
![image](https://user-images.githubusercontent.com/25688193/34608611-7752d58c-f25c-11e7-8e9c-0ea0223b6809.png)
![image](https://user-images.githubusercontent.com/25688193/34608723-0c873b3e-f25d-11e7-9fa6-d7af3166bfa9.png)


<a id="ID_10-5-1-2"></a>

#### 符号化器 - 再帰層 [encoder - recurrent layer]
![image](https://user-images.githubusercontent.com/25688193/34613719-1bc6267c-f272-11e7-9ab8-abb1b5edf9a7.png)
![image](https://user-images.githubusercontent.com/25688193/34613470-46fdc670-f271-11e7-9642-cb697fd13e38.png)
![image](https://user-images.githubusercontent.com/25688193/34616511-d9326500-f27b-11e7-8c71-cfbb2afdf7c6.png)


<a id="ID_10-5-1-3"></a>

#### 復号化器 - 埋め込み層 [decoder - embedding layer]
![image](https://user-images.githubusercontent.com/25688193/34621002-d05135d8-f28a-11e7-9874-5e61dc3bff78.png)
![image](https://user-images.githubusercontent.com/25688193/34621826-02ce7612-f28e-11e7-8779-0c54ee260eca.png)
![image](https://user-images.githubusercontent.com/25688193/34621841-0fce3244-f28e-11e7-9e9b-9acfc2f3a42c.png)
![image](https://user-images.githubusercontent.com/25688193/34622123-37cdb50c-f28f-11e7-8866-7fbe46176930.png)
![image](https://user-images.githubusercontent.com/25688193/34622771-d1af7276-f291-11e7-99fa-17570a7b5da0.png)


<a id="ID_10-5-1-4"></a>

#### 復号化器 - 再帰層 [decoder - recurrent layer]
![image](https://user-images.githubusercontent.com/25688193/34633555-30873486-f2c0-11e7-80b2-47e987f1a9f9.png)
![image](https://user-images.githubusercontent.com/25688193/34633705-35032e6a-f2c1-11e7-8400-c8ea9c24a9bd.png)
![image](https://user-images.githubusercontent.com/25688193/34633778-b26695c2-f2c1-11e7-945e-d11f343edb5c.png)



<a id="ID_10-5-1-5"></a>

#### 復号化器 - 出力層 [decoder - output layer]
![image](https://user-images.githubusercontent.com/25688193/34634962-c7f7ea84-f2cc-11e7-894e-b92866e0cbb5.png)
![image](https://user-images.githubusercontent.com/25688193/34638559-4d84ce94-f311-11e7-862e-e69b9da0a817.png)
![image](https://user-images.githubusercontent.com/25688193/34638605-3f0fb274-f312-11e7-98d4-9e9faef01c07.png)
![image](https://user-images.githubusercontent.com/25688193/34638638-52b5736c-f313-11e7-8edd-354fdfec4164.png)
![image](https://user-images.githubusercontent.com/25688193/34638773-494645a6-f316-11e7-9e30-a227217e792e.png)
![image](https://user-images.githubusercontent.com/25688193/34638779-58512a3e-f316-11e7-8ab3-79fcd64861f1.png)


<a id="ID_10-5-1-6"></a>

#### seq2seq モデルの処理負荷
![image](https://user-images.githubusercontent.com/25688193/34639510-b99b87cc-f324-11e7-928a-7ffa3338dfb3.png)
![image](https://user-images.githubusercontent.com/25688193/34639540-19586180-f325-11e7-91f8-847c6525411d.png)
![image](https://user-images.githubusercontent.com/25688193/34639601-fa734a0e-f325-11e7-9fc1-b134af486d23.png)


<a id="ID_10-5-2"></a>

### seq2seq モデルの学習方法
![image](https://user-images.githubusercontent.com/25688193/34640845-0fb58cac-f33e-11e7-8cbd-c9b7cd2e9f82.png)
![image](https://user-images.githubusercontent.com/25688193/34640850-226d2b34-f33e-11e7-804f-7836d47a381f.png)
![image](https://user-images.githubusercontent.com/25688193/34640867-56627656-f33e-11e7-9cd4-6d59847c0995.png)



<a id="ID_10-5-3"></a>

### seq2seq モデルにおける系列生成方法
![image](https://user-images.githubusercontent.com/25688193/34642354-da54afcc-f354-11e7-96b9-440995d2cec9.png)
![image](https://user-images.githubusercontent.com/25688193/34642427-28714d22-f356-11e7-946d-fae442965ecd.png)
![image](https://user-images.githubusercontent.com/25688193/34642432-3bc8b1ee-f356-11e7-864f-7cdd079d0778.png)


<a id="ID_10-5-3-1"></a>

### 貪欲法 [greedy algorithm]
![image](https://user-images.githubusercontent.com/25688193/34643612-9610d6f4-f36a-11e7-9b7c-cb2bacc29142.png)
![image](https://user-images.githubusercontent.com/25688193/34643418-4e1891fa-f367-11e7-8e6c-10de1d339b83.png)
![image](https://user-images.githubusercontent.com/25688193/34643427-731d22d6-f367-11e7-86b6-9a419cf2e752.png)


<a id="ID_10-5-3-2"></a>

### ビーム探索 [beam search]
![image](https://user-images.githubusercontent.com/25688193/34643891-d5fb49f2-f36f-11e7-8a93-7f2600ea0462.png)
![image](https://user-images.githubusercontent.com/25688193/34645034-20624a6a-f387-11e7-9133-076f88584d59.png)
![image](https://user-images.githubusercontent.com/25688193/34645036-3ccbb52e-f387-11e7-9252-b9bd0209185a.png)
![image](https://user-images.githubusercontent.com/25688193/34645021-9fed1946-f386-11e7-890e-dead39aeadbe.png)
![image](https://user-images.githubusercontent.com/25688193/34645090-2569e2a6-f388-11e7-903d-909b47bafc81.png)
![image](https://user-images.githubusercontent.com/25688193/34645212-b9593708-f38a-11e7-8c5f-d2224fd9e242.png)
![image](https://user-images.githubusercontent.com/25688193/34645279-6a4b90a0-f38c-11e7-88a1-363a7d4f6e7d.png)
![image](https://user-images.githubusercontent.com/25688193/34645282-7bb1eab0-f38c-11e7-8d26-bfe836081ed5.png)
![image](https://user-images.githubusercontent.com/25688193/34645358-15c1dfba-f38e-11e7-9540-450af4e5f89d.png)
![image](https://user-images.githubusercontent.com/25688193/34645366-2b706b1a-f38e-11e7-879a-3f818bcde521.png)

- 参考サイト
    - https://deepage.net/machine_learning/2017/07/06/beam-search.html
    - http://www.phontron.com/slides/nlp-programming-ja-13-search.pdf

---

<a id="ID_10-6"></a>

## 注意機構 [attention mechanism] / seq2seq model
![image](https://user-images.githubusercontent.com/25688193/34693672-f3eb3406-f507-11e7-89eb-3db1a71aafc3.png)

<a id="ID_10-6-1"></a>

### ソフト注意機構 [soft attention mechanism]

<a id="ID_10-6-1-1"></a>

#### seq2seq モデルでのソフト注意機構 [soft attention mechanism]
![image](https://user-images.githubusercontent.com/25688193/34696507-70cce974-f512-11e7-92b1-ebf653b546a0.png)
![image](https://user-images.githubusercontent.com/25688193/34714577-317fa986-f56d-11e7-8eea-a5893ccf713e.png)
![image](https://user-images.githubusercontent.com/25688193/34712835-94e0d88e-f567-11e7-9ce4-125a8988785a.png)
![image](https://user-images.githubusercontent.com/25688193/34715071-b964afc6-f56e-11e7-85a9-83a96ea2d255.png)
![image](https://user-images.githubusercontent.com/25688193/34715658-ae0f2df2-f570-11e7-8e85-f735ea4c7868.png)
![image](https://user-images.githubusercontent.com/25688193/34720596-a12f67a2-f582-11e7-9670-517cd6e06dba.png)
![image](https://user-images.githubusercontent.com/25688193/34720614-b5bd33b6-f582-11e7-8463-f696271bd4ed.png)


<a id="ID_10-6-1-2"></a>

#### より一般的なモデルでのソフト注意機構 [soft attention mechanism]
![image](https://user-images.githubusercontent.com/25688193/34725022-1309d96a-f593-11e7-854a-02d68f7e91d0.png)
![image](https://user-images.githubusercontent.com/25688193/34725002-00ae1402-f593-11e7-8029-14b6345ca32d.png)
![image](https://user-images.githubusercontent.com/25688193/34725150-64668858-f593-11e7-9bfe-185022357b39.png)
![image](https://user-images.githubusercontent.com/25688193/34725915-c9124a42-f595-11e7-904f-79aa48b24760.png)
![image](https://user-images.githubusercontent.com/25688193/34726005-15c4a1fa-f596-11e7-9ba5-d4467bcf9a9e.png)


<a id="ID_10-6-2"></a>

### ハード注意機構 [hard attention mechanism]
![image](https://user-images.githubusercontent.com/25688193/34737255-fcb9a2a0-f5b8-11e7-8de3-48149b2015e5.png)
![image](https://user-images.githubusercontent.com/25688193/34747848-4b833aa8-f5dd-11e7-9748-db4567d1f086.png)
![image](https://user-images.githubusercontent.com/25688193/34747891-795bb4d2-f5dd-11e7-9467-b1a940080f47.png)

> 記載中...

---

<a id="ID_10-7"></a>

## 記憶ネットワーク [MemN : memory networks]

- 参照サイト
    - http://deeplearning.hatenablog.com/entry/memory_networks

![image](https://user-images.githubusercontent.com/25688193/34750579-12688b7a-f5eb-11e7-9138-a71232566b83.png)


<a id="ID_10-7-0"></a>

### 記憶ネットワークのアーキテクチャ [architecture]
![image](https://user-images.githubusercontent.com/25688193/34772531-937af814-f64b-11e7-94ff-0b7dfce9d10b.png)
![image](https://user-images.githubusercontent.com/25688193/34772845-dae746ac-f64c-11e7-9417-b2d3b595f4cc.png)
![image](https://user-images.githubusercontent.com/25688193/34773668-db0625ec-f64f-11e7-81ee-9a83fa637bef.png)
![image](https://user-images.githubusercontent.com/25688193/34773684-e8e57d84-f64f-11e7-8f20-39b31cc65c6f.png)


<a id="ID_10-7-1"></a>

### 教師あり記憶ネットワーク [supervised memory networks / strongly supervised memory networks]
![image](https://user-images.githubusercontent.com/25688193/34781151-6e4f4316-f668-11e7-905f-8e21988614e0.png)
![image](https://user-images.githubusercontent.com/25688193/34781680-d11b4cc8-f669-11e7-8b32-e7624d2d2d07.png)

<a id="ID_10-7-1-1"></a>

#### I : 入力情報変換 [input feature map]
![image](https://user-images.githubusercontent.com/25688193/34785928-e5e169ce-f675-11e7-9713-fe150cffa3e0.png)

<a id="ID_10-7-1-2"></a>

#### G : 一般化 [genelarization]
![image](https://user-images.githubusercontent.com/25688193/34785947-f4d3b806-f675-11e7-809b-27f9e367d403.png)

<a id="ID_10-7-1-3"></a>

#### O : 出力情報変換 [output feature map]
![image](https://user-images.githubusercontent.com/25688193/34796301-6fa16d4a-f698-11e7-9149-bc0f36e47a4c.png)
![image](https://user-images.githubusercontent.com/25688193/34796406-cae41d06-f698-11e7-94d5-f10b63f590a9.png)
![image](https://user-images.githubusercontent.com/25688193/34797118-c073ab78-f69a-11e7-82a1-2d11326e27f5.png)
![image](https://user-images.githubusercontent.com/25688193/34799590-c00e3776-f6a3-11e7-95c5-e594980bb46e.png)
![image](https://user-images.githubusercontent.com/25688193/34799819-a2c2e148-f6a4-11e7-8c3c-8ea9bdd885de.png)
![image](https://user-images.githubusercontent.com/25688193/34800341-9f92123a-f6a6-11e7-910e-11e3df0d085c.png)
![image](https://user-images.githubusercontent.com/25688193/34804317-5e305f94-f6bb-11e7-86f5-596e3e1d0fff.png)


<a id="ID_10-7-2"></a>

### end-to-end 記憶ネットワーク [end-to-end memory networks]
![image](https://user-images.githubusercontent.com/25688193/34809894-6889c384-f6db-11e7-9910-b7bba39c21f9.png)
![image](https://user-images.githubusercontent.com/25688193/34819999-b3525f3a-f702-11e7-8b82-177b1e6eb82a.png)
![image](https://user-images.githubusercontent.com/25688193/34815299-2f80cdc6-f6f4-11e7-8372-77426d2c5fa0.png)

<a id="ID_10-7-2-1"></a>

#### I : 入力情報変換 [input feature map]
![image](https://user-images.githubusercontent.com/25688193/34816109-3e821ef8-f6f7-11e7-8b86-117d0681c367.png)

<a id="ID_10-7-2-2"></a>

#### G : 一般化 [genelarization]
![image](https://user-images.githubusercontent.com/25688193/34823860-836fb5ee-f70f-11e7-8472-caee3ad07d7d.png)

<a id="ID_10-7-2-3"></a>

#### O : 出力情報変換 [output feature map]
![image](https://user-images.githubusercontent.com/25688193/34820056-dd95b954-f702-11e7-8315-a6aa4f5fa315.png)
![image](https://user-images.githubusercontent.com/25688193/34819409-ff813ac2-f700-11e7-8ca3-7ef3598ddd9e.png)


<a id="ID_10-7-3"></a>

### 動的記憶ネットワーク [DMN : dynamic memory networks]
![image](https://user-images.githubusercontent.com/25688193/34824992-0b69ac08-f714-11e7-8b27-d0c4ebada20f.png)
![image](https://user-images.githubusercontent.com/25688193/34824969-f635b660-f713-11e7-9bf2-e3ce870a3384.png)
![image](https://user-images.githubusercontent.com/25688193/34825462-ebdb781a-f715-11e7-9e82-141d1322cef7.png)
![image](https://user-images.githubusercontent.com/25688193/34827254-e18bcc96-f71c-11e7-8ace-f0012a4cd09c.png)
![image](https://user-images.githubusercontent.com/25688193/34827387-5673a286-f71d-11e7-8e0b-7172cb38c394.png)

---

<a id="ID_10-8"></a>

## ニューラル言語モデル、seq2seq モデルの出力層の高速化手法<br>（クロス・エントロピー損失関数の勾配計算の効率化）
![image](https://user-images.githubusercontent.com/25688193/34836700-0a3204fc-f73c-11e7-80b2-30ee6470926a.png)

![image](https://user-images.githubusercontent.com/25688193/34839746-0c4adfca-f746-11e7-887c-077708159ed8.png)
![image](https://user-images.githubusercontent.com/25688193/34863777-82e0640c-f7b4-11e7-8d81-bbea2dc425d2.png)
![image](https://user-images.githubusercontent.com/25688193/34863807-a539b08a-f7b4-11e7-883b-2087d238bc22.png)
![image](https://user-images.githubusercontent.com/25688193/34864657-9fe11b74-f7b8-11e7-9716-3487c83d6aa7.png)
![image](https://user-images.githubusercontent.com/25688193/34864820-6c38c9ec-f7b9-11e7-95f6-69d36b8103ff.png)


<a id="ID_10-8-1"></a>

### 重点サンプリング [importance sampling]
![image](https://user-images.githubusercontent.com/25688193/34873490-990a2bea-f7d8-11e7-9e64-5b816058eeb4.png)
![image](https://user-images.githubusercontent.com/25688193/34896933-03995c78-f82f-11e7-8e9a-b3837adad5ee.png)
![image](https://user-images.githubusercontent.com/25688193/34896996-3dc27164-f82f-11e7-8c0b-f038a0fd9cc3.png)
![image](https://user-images.githubusercontent.com/25688193/34897240-74b5bf86-f830-11e7-95f1-0670056dcfe5.png)
![image](https://user-images.githubusercontent.com/25688193/34898714-d5df75fc-f837-11e7-8a2e-19c4226ec8eb.png)
![image](https://user-images.githubusercontent.com/25688193/34903184-9852811a-f86f-11e7-968c-4e31fa1085cd.png)
![image](https://user-images.githubusercontent.com/25688193/34903344-7e732120-f872-11e7-92ac-99fb3c407e9b.png)
![image](https://user-images.githubusercontent.com/25688193/34918786-09ce01de-f99c-11e7-9186-2019a1a25266.png)


<a id="ID_10-8-2"></a>

### 雑音対照推定 [NCE : noise-contrastive estimation]
![image](https://user-images.githubusercontent.com/25688193/34910831-7e095c34-f900-11e7-9627-f747296bd2ff.png)
![image](https://user-images.githubusercontent.com/25688193/34910839-a4f26d68-f900-11e7-82b8-488303fe0e73.png)

![image](https://user-images.githubusercontent.com/25688193/34910914-d72e3f90-f901-11e7-8ff4-91060680a638.png)
![image](https://user-images.githubusercontent.com/25688193/34910933-26e09308-f902-11e7-94a2-41c23bf07579.png)
![image](https://user-images.githubusercontent.com/25688193/34911105-f320dee8-f905-11e7-98a5-4f9231be28ff.png)

- 参考サイト
    - https://qiita.com/Quasi-quant2010/items/a15b0d1b6428dc49c6c2


<a id="ID_10-8-3"></a>

### 負例サンプリング [negative sampling]
![image](https://user-images.githubusercontent.com/25688193/34918212-995f4600-f992-11e7-8db7-69a9677a48d5.png)
![image](https://user-images.githubusercontent.com/25688193/34916162-ca94c87e-f976-11e7-8e36-b749d26f45ab.png)
![image](https://user-images.githubusercontent.com/25688193/34916265-c2ad5da4-f978-11e7-9f63-3e5c7159616f.png)


<a id="ID_10-8-4"></a>

### ブラックアウト [black-out]
![image](https://user-images.githubusercontent.com/25688193/34918300-c4f711de-f993-11e7-879a-38c6eb558859.png)
![image](https://user-images.githubusercontent.com/25688193/34918493-a15bed00-f996-11e7-9bd0-20e22b6be5c0.png)
![image](https://user-images.githubusercontent.com/25688193/34918847-35f9b892-f99d-11e7-92de-53ecf1ee388c.png)
![image](https://user-images.githubusercontent.com/25688193/34918861-6971d056-f99d-11e7-9f28-35c4330b307a.png)

![image](https://user-images.githubusercontent.com/25688193/34922645-0e1ec608-f9d6-11e7-96b2-8742708da58d.png)
![image](https://user-images.githubusercontent.com/25688193/34922650-21c70bc0-f9d6-11e7-99c4-65eb54f07304.png)


<a id="ID_10-8-5"></a>

### 階層的ソフトマックス [HSM : hierarchial softmax]
![image](https://user-images.githubusercontent.com/25688193/34958572-d752d484-fa75-11e7-98ed-a0f58e84084a.png)
![image](https://user-images.githubusercontent.com/25688193/34960208-42222d12-fa7d-11e7-9889-105a86fe3e4a.png)
![image](https://user-images.githubusercontent.com/25688193/34960422-12046324-fa7e-11e7-8ebe-d6d0c59314bd.png)
![image](https://user-images.githubusercontent.com/25688193/34968754-7aebfd2c-faae-11e7-8106-2cb6946def24.png)


<a id="ID_10-8-6"></a>

### 各種高速化手法の比較
> 記載中...


---


<a id="ID_10-9"></a>

## 自然言語処理の応用タスク [application]


<a id="ID_10-9-1"></a>

### 機械翻訳 [MT : machine translation]


<a id="ID_10-9-1-1"></a>

#### GroundHog / RNNSearch
- 参考サイト
    - （公式）https://github.com/lisa-groundhog/GroundHog

モントリオール大学からリリースされているニューラル翻訳（NMT）のツール。<br>
GroundHog ツールのモデルの実装は、注意機構 [attention] 有りとなし両方の場合を含む。

<a id="ID_10-9-1-2"></a>

#### OpenNMT / seq2seq-attn
- 参考サイト
    - （公式）http://opennmt.net/
    - GitHub : https://github.com/opennmt/opennmt

ツールの使い方は、上記の参考サイトにて。<br>
以下は、OpenNMT ツールで採用されているモデルのアーキテクチャの説明。

![image](https://user-images.githubusercontent.com/25688193/34982479-d83aa4c6-faed-11e7-9b7b-c01cef081725.png)

<a id="ID_10-9-1-2-1"></a>

#### 符号化器 [Encoder] / 2 層の Bidirectional-LSTM
![image](https://user-images.githubusercontent.com/25688193/34982503-e8f7f4d0-faed-11e7-8dd7-1ce3d7e137d4.png)
![image](https://user-images.githubusercontent.com/25688193/34981388-b7bfd2be-faea-11e7-997c-95c48b9d7e09.png)

##### 符号化器 - 埋め込み層 [encoder - embedding layer]
![image](https://user-images.githubusercontent.com/25688193/34982208-1f4a38be-faed-11e7-81a3-34f5f88537e2.png)

##### 符号化器 - 再帰層 [encoder - recurrent layer]
![image](https://user-images.githubusercontent.com/25688193/34983659-9dc8b8ce-faf1-11e7-8592-4ab440654e0d.png)
![image](https://user-images.githubusercontent.com/25688193/34984444-598654b6-faf4-11e7-8418-ef09c7728b60.png)


<a id="ID_10-9-1-2-2"></a>

#### 復号化器 [Decoder] / 2 層の LSTM + attention 層
![image](https://user-images.githubusercontent.com/25688193/35031279-917b1896-fba5-11e7-8dae-4f482846f1a4.png)
![image](https://user-images.githubusercontent.com/25688193/35039068-1b08cf26-fbc0-11e7-91cb-a506a7d9cbd5.png)

![image](https://user-images.githubusercontent.com/25688193/35039784-4419aaa0-fbc2-11e7-87c1-d9d30015d22e.png)

![image](https://user-images.githubusercontent.com/25688193/35040247-c12aa35e-fbc3-11e7-8bb8-25a9fa2b052e.png)


##### 復号化器 - 埋め込み層 [decoder - recurrent layer]
![image](https://user-images.githubusercontent.com/25688193/35101821-3fe6946a-fca4-11e7-9c83-d85f0af193ea.png)
![image](https://user-images.githubusercontent.com/25688193/35041847-8edad90e-fbc9-11e7-88d8-c3fd44efae50.png)

##### 復号化器 - 再帰層 [decoder - recurrent layer]
![image](https://user-images.githubusercontent.com/25688193/35042645-d6312af8-fbcc-11e7-85dc-36c40861b4d7.png)
![image](https://user-images.githubusercontent.com/25688193/35042331-9c34714e-fbcb-11e7-963a-26cef53c54ae.png)
![image](https://user-images.githubusercontent.com/25688193/35043091-9799e544-fbce-11e7-8df0-3cf6ef7187ce.png)

##### 復号化器 - 注意層 [decoder - attention layer]
![image](https://user-images.githubusercontent.com/25688193/35101699-c9e86400-fca3-11e7-8dd8-708f929a50c9.png)
![image](https://user-images.githubusercontent.com/25688193/35058382-21af2f7e-fbfb-11e7-91eb-0735cdd38e2b.png)
![image](https://user-images.githubusercontent.com/25688193/35216508-32a66280-ffab-11e7-8889-db89e8e8960c.png)

##### 復号化器 - 出力層 [decoder - output layer] / モデルの学習時の処理
![image](https://user-images.githubusercontent.com/25688193/35102186-774b92b0-fca5-11e7-9710-90a3efc635d2.png)
![image](https://user-images.githubusercontent.com/25688193/35102671-eb8f7320-fca6-11e7-9c4e-ca1f1672e21f.png)

##### 復号化器 - 出力層 [decoder - output layer] / モデルの評価時の処理
![image](https://user-images.githubusercontent.com/25688193/35101875-6fa30aa8-fca4-11e7-823b-a69ccb245c34.png)
![image](https://user-images.githubusercontent.com/25688193/35103395-094634d8-fca9-11e7-9965-f892f98ff7c3.png)


<a id="ID_10-9-1-3"></a>

#### 機械翻訳タスクで共通の課題とその対策、改良
![image](https://user-images.githubusercontent.com/25688193/35150308-4e2b76a8-fd5d-11e7-9330-71d3084972d6.png)

<a id="ID_10-9-1-3-1"></a>

##### 語彙数、未知語と入出力単位
![image](https://user-images.githubusercontent.com/25688193/35152023-fc0ad5b0-fd63-11e7-9629-9a52a76cc8e0.png)
![image](https://user-images.githubusercontent.com/25688193/35152048-166a6236-fd64-11e7-885a-bd3126ea1a21.png)
![image](https://user-images.githubusercontent.com/25688193/35152078-35991d82-fd64-11e7-8816-a7de70924572.png)
![image](https://user-images.githubusercontent.com/25688193/35152094-48168364-fd64-11e7-85a2-c6b4353624ab.png)
![image](https://user-images.githubusercontent.com/25688193/35152105-57f2e91c-fd64-11e7-8cb6-f8ef9a686f81.png)

<a id="ID_10-9-1-3-2"></a>

##### 過剰生成 [over-generation]、不足生成 [under-generation] と被覆 [coverage]
![image](https://user-images.githubusercontent.com/25688193/35171771-50dd27e8-fda8-11e7-83f7-941dfbb7a448.png)
![image](https://user-images.githubusercontent.com/25688193/35178696-ec175996-fdcf-11e7-8baa-2abfba59fbb2.png)

- 元論文「Modeling Coverage for Neural Machine Translation」
    - arXiv.org : https://arxiv.org/abs/1601.04811

---

<a id="ID_10-9-2"></a>

### 文書要約 [text summarization]

- 参考サイト
    - [Qiita : 大自然言語時代のための、文章要約](https://qiita.com/icoxfog417/items/d06651db10e27220c819)

![image](https://user-images.githubusercontent.com/25688193/35188859-f2bc993e-fe81-11e7-97a4-37da93881cfe.png)

<a id="ID_10-9-2-1"></a>

#### 見出し生成タスク [headline generation task] / 短文生成タスク
![image](https://user-images.githubusercontent.com/25688193/35188863-08440b20-fe82-11e7-9190-7b645293f036.png)

<a id="ID_10-9-2-1-1"></a>

#### 文書要約タスクでの Encoder-Decoder 方式 / attention 構造を用いるモデル
![image](https://user-images.githubusercontent.com/25688193/35188731-cfb5ee8e-fe7e-11e7-99fb-9af2d63021a7.png)

<a id="ID_10-9-2-1-1-1"></a>

#### 「A Neural Attention Model for Abstractive Sentence Summarization」/ Attention-Based Summarization (ABS)

- 元論文「A Neural Attention Model for Abstractive Sentence Summarization」
    - arxv.org : https://arxiv.org/abs/1509.00685
- 実装
    - [GitHub : facebookarchive/NAMAS](https://github.com/facebookarchive/NAMAS)

![image](https://user-images.githubusercontent.com/25688193/35189017-65a1679c-fe85-11e7-9706-a5a355cf45fe.png)
![image](https://user-images.githubusercontent.com/25688193/35189030-d97cca44-fe85-11e7-9e4e-d9505926f693.png)
![image](https://user-images.githubusercontent.com/25688193/35196552-ed72d1e2-ff16-11e7-8208-34b91c2f6597.png)

##### 順伝播ニューラル言語モデル側のアーキテクチャ
![image](https://user-images.githubusercontent.com/25688193/35191638-5dfb9326-fec3-11e7-8491-8028d0e64099.png)
![image](https://user-images.githubusercontent.com/25688193/35198549-cfa7ea86-ff33-11e7-9490-febafe0ab697.png)
![image](https://user-images.githubusercontent.com/25688193/35198561-f7edae86-ff33-11e7-8d4d-301c1f4defbc.png)

##### attention 構造付き Encoder 側のアーキテクチャ
![image](https://user-images.githubusercontent.com/25688193/35196705-2fae63c6-ff19-11e7-87d9-f59c43236f93.png)
![image](https://user-images.githubusercontent.com/25688193/35204835-22f632ca-ff74-11e7-946c-99dfd62c879e.png)
![image](https://user-images.githubusercontent.com/25688193/35216185-1aa58c34-ffaa-11e7-89ea-388821bcf956.png)

---

<a id="ID_10-9-2-1-2"></a>

#### RNN による ABS モデルの拡張、改良

- 元論文「Abstractive Sentence Summarization with Attentive Recurrent Neural Networks」
- 元論文「Sequence-to-sequence RNNs for text summarization」
- 元論文「Abstractive Text Summarization Using Sequence-to-Sequence RNNs and Beyond」
    - arix.org : https://arxiv.org/abs/1602.06023

![image](https://user-images.githubusercontent.com/25688193/35223499-ebfe18d6-ffc4-11e7-9920-48bde479e3e6.png)

---

<a id="ID_10-9-3"></a>

### 対話システム [dialog system]
- 参考サイト
    - [Qiita : 機械学習を使って作る対話システム](https://qiita.com/Hironsan/items/6425787ccbee75dfae36)

![image](https://user-images.githubusercontent.com/25688193/35259767-f2b75d82-004a-11e8-9247-23172ac4f409.png)

<a id="ID_10-9-3-1"></a>

#### 対話モデル
![image](https://user-images.githubusercontent.com/25688193/35252401-a389e17a-0023-11e8-9db0-1377807771c4.png)
![image](https://user-images.githubusercontent.com/25688193/35259787-11dfe38c-004b-11e8-8b79-9e400d9c097b.png)

<a id="ID_10-9-3-1-1"></a>

##### 対話システムにおける seq2seq モデルの適用
![image](https://user-images.githubusercontent.com/25688193/35260583-b6751d46-004f-11e8-9af0-734329e3427c.png)
![image](https://user-images.githubusercontent.com/25688193/35260601-c4a358b0-004f-11e8-9a26-ca859d9add8e.png)
![image](https://user-images.githubusercontent.com/25688193/35263139-fb2e4646-005a-11e8-827b-a5189e5486d4.png)

<a id="ID_10-9-3-1-2"></a>

##### attention 構造を用いた、対話モデル
![image](https://user-images.githubusercontent.com/25688193/35263175-1a03d022-005b-11e8-84eb-76a0cbf2fc21.png)

- 元論文「Neural Responding Machine for Short-Text Conversation」
    - arXiv.org : https://arxiv.org/abs/1503.02364

<a id="ID_10-9-3-1-3"></a>

##### 対話システムの特徴である話者交代と発話者を積極的にモデルに取り組んだ手法
![image](https://user-images.githubusercontent.com/25688193/35263771-6fd71548-005d-11e8-8c9d-f7e2d36f677a.png)

- 元論文「Building End-To-End Dialogue Systems Using Generative Hierarchical Neural Network Models」
    - arXiv.org : https://arxiv.org/abs/1507.04808
- 元論文「A Persona-Based Neural Conversation Model」
    - arXiv.org : https://arxiv.org/abs/1603.06155
    - GitHub : https://github.com/jiweil/Neural-Dialogue-Generation
- 元論文「Addressee and Response Selection for Multi-Party Conversation」
    - pdf : https://www.aclweb.org/anthology/D16-1231

##### 論文「Building End-To-End Dialogue Systems Using Generative Hierarchical Neural Network Models」
![image](https://user-images.githubusercontent.com/25688193/35306559-acea0696-00e1-11e8-9d8a-f065c3100d0d.png)
![image](https://user-images.githubusercontent.com/25688193/35311154-6847cb88-00f8-11e8-8315-21a451642256.png)

##### 論文「A Persona-Based Neural Conversation Model」
![image](https://user-images.githubusercontent.com/25688193/35312961-4c43197a-0101-11e8-91c9-e69c79d455e3.png)
![image](https://user-images.githubusercontent.com/25688193/35312974-615426f6-0101-11e8-8ae6-650d4b6af7d0.png)
![image](https://user-images.githubusercontent.com/25688193/35313317-064a0df0-0103-11e8-812e-452d513a9b7d.png)

##### 論文「Addressee and Response Selection for Multi-Party Conversation」
![image](https://user-images.githubusercontent.com/25688193/35315271-d243e4f2-010e-11e8-90f5-3ed3f6b03726.png)
![image](https://user-images.githubusercontent.com/25688193/35315278-e03b4744-010e-11e8-8f78-846c297a0879.png)
![image](https://user-images.githubusercontent.com/25688193/35316317-4bce7b0c-0114-11e8-8f26-c33d95b3d6dc.png)


<a id="ID_10-9-3-2"></a>

#### 対話モデルの発展
![image](https://user-images.githubusercontent.com/25688193/35375660-33403454-01eb-11e8-904a-0a005721b951.png)

> 記載中...


<a id="ID_10-9-3-3"></a>

#### 対話システムの自動評価
![image](https://user-images.githubusercontent.com/25688193/35375628-0e03c872-01eb-11e8-98a1-91188223fe28.png)
![image](https://user-images.githubusercontent.com/25688193/35375963-4ec5b81a-01ec-11e8-9900-ed470d78369c.png)

##### 論文「The Ubuntu Dialogue Corpus: A Large Dataset for Research in Unstructured Multi-Turn Dialogue Systems」
- 元論文「The Ubuntu Dialogue Corpus: A Large Dataset for Research in Unstructured Multi-Turn Dialogue Systems」
    - arXiv.org : https://arxiv.org/abs/1506.08909

![image](https://user-images.githubusercontent.com/25688193/35376612-2bd0ebf6-01ef-11e8-93dc-ed95f5061ad7.png)
![image](https://user-images.githubusercontent.com/25688193/35379682-31f66780-01fa-11e8-8705-9bf35f1099c4.png)
![image](https://user-images.githubusercontent.com/25688193/35380799-a6e7fcf4-01fd-11e8-83d7-ffae2b5e7a49.png)
![image](https://user-images.githubusercontent.com/25688193/35380914-fa06e724-01fd-11e8-834a-1b859d750bd6.png)


---

<a id="ID_10-9-4"></a>

### 質問応答 [QA : question answering]
![image](https://user-images.githubusercontent.com/25688193/35413620-629477ba-0263-11e8-8f63-cf62ebadbaf8.png)
![image](https://user-images.githubusercontent.com/25688193/35414383-a9ab6724-0265-11e8-9e88-7d9ba0ae0721.png)

<a id="ID_10-9-4-1"></a>

#### 回答選択タスク
![image](https://user-images.githubusercontent.com/25688193/35424973-ab44958a-029a-11e8-90de-c73a4bcbaf1d.png)
![image](https://user-images.githubusercontent.com/25688193/35425988-f5f067c8-02a2-11e8-88be-8f532372466c.png)
![image](https://user-images.githubusercontent.com/25688193/35428536-f60ddeec-02b2-11e8-8518-342fc92dfef4.png)
![image](https://user-images.githubusercontent.com/25688193/35428542-0312d390-02b3-11e8-8eeb-39eeab0b146b.png)

この際に行われる、質問文と回答候補のベクトル表現化の手法としては、以下のような手法が挙げられる。
- 双方向 LSTM により、文のベクトルを単一のベクトルに変換（符号化）
    - 元論文「LSTM-based Deep Learning Models for Non-factoid Answer Selection」
        - arXiv.org : https://arxiv.org/abs/1511.04108
    - 元論文「A Long Short-Term Memory Model for Answer Sentence Selection in. Question Answering」
- 木構造再帰ニューラルネットワークにより、文のベクトルを単一のベクトルに変換（符号化）
    - 元論文「A Neural Network for Factoid Question Answering over Paragraphs」
- 畳み込みニューラルネットワークにより、文のベクトルを単一のベクトルに変換（符号化）
    - 元論文「Applying Deep Learning to Answer Selection: A Study and An Open Task」
        - arXiv.org : https://arxiv.org/abs/1508.01585
    - 元論文「Deep Learning for Answer Sentence Selection」
        - arXiv.org : https://arxiv.org/abs/1412.1632

より発展させたモデルでは、
- CNN で出力された複数ベクトルに対し、LSTM を適用して、文のベクトルを単一のベクトルに変換（符号化）
    - 元論文「LSTM-based Deep Learning Models for Non-factoid Answer Selection」<br>（先の双方向 LSTM での手法と同じ論文）
        - arXiv.org : https://arxiv.org/abs/1511.04108
- 注意機構 [attention] との組み合わせる
    - 元論文「aNMM: Ranking Short Answer Texts with Attention-Based Neural Matching Model」
        - arXiv.org : https://arxiv.org/abs/1801.01641
- パラメータの異なる CNN での結果を組み合わせる
    - 元論文「Multi-Perspective Sentence Similarity Modeling with Convolutional Neural Networks」

最近の傾向としては、CNN をベースに改良したモデルが高い精度を出している傾向がある。<br>
このように、文レベルのベクトル表現（符号化）手法は、新たな手法が次々に出ている状況であり、今後も工夫の余地が大きいと考えられる。

![image](https://user-images.githubusercontent.com/25688193/35429343-07b10eb8-02b7-11e8-9beb-8a9a60b330c4.png)
![image](https://user-images.githubusercontent.com/25688193/35452896-886cd7ea-030b-11e8-9a48-eefdfd588866.png)
![image](https://user-images.githubusercontent.com/25688193/35452997-eb1a8c52-030b-11e8-84da-84c676c2b84a.png)

<a id="ID_10-9-4-2"></a>

#### 回答選択問題の評価方法
![image](https://user-images.githubusercontent.com/25688193/35465079-e2741c22-033c-11e8-9319-b07df0f90438.png)
![image](https://user-images.githubusercontent.com/25688193/35470418-7ba4bfa6-038c-11e8-8da3-019087dc1262.png)
![image](https://user-images.githubusercontent.com/25688193/35470413-64e60f7c-038c-11e8-80a0-e3c4f8f1fd72.png)

<a id="ID_10-9-4-3"></a>

#### end-to-end な質問応答
![image](https://user-images.githubusercontent.com/25688193/35471116-8cfc3a52-0398-11e8-8f17-09c8b4742cd9.png)

- bAbI「Towards AI-Complete Question Answering: A Set of Prerequisite Toy Tasks」
    - arXiv.org : https://arxiv.org/abs/1502.05698
    - https://research.fb.com/downloads/babi/
    - https://github.com/facebook/bAbI-tasks

<br>

---

<a name="参考文献"></a>

## 参考文献

> 深層学習: Deep Learning</br>
> [amazonで詳細を見る](https://www.amazon.co.jp/%E6%B7%B1%E5%B1%A4%E5%AD%A6%E7%BF%92-Deep-Learning-%E7%9B%A3%E4%BF%AE-%E4%BA%BA%E5%B7%A5%E7%9F%A5%E8%83%BD%E5%AD%A6%E4%BC%9A/dp/476490487X)

> 詳解 ディープラーニング ~ TensorFlow・Keras による時系列データ処理</br>
> [amazonで詳細を見る](https://www.amazon.co.jp/exec/obidos/ASIN/4839962510/hikarus0sem0y-22/)<br>
>> 本書のレビュー記事 :<br> 
>> [【書籍紹介】詳解ディープラーニング TensorFlow・Kerasによる時系列データ処理](http://s0sem0y.hatenablog.com/entry/2017/06/25/025725)

> 深層学習による自然言語処理 (機械学習プロフェッショナルシリーズ) <br>
> [amazonで詳細を見る](https://www.amazon.co.jp/%E6%B7%B1%E5%B1%A4%E5%AD%A6%E7%BF%92%E3%81%AB%E3%82%88%E3%82%8B%E8%87%AA%E7%84%B6%E8%A8%80%E8%AA%9E%E5%87%A6%E7%90%86-%E6%A9%9F%E6%A2%B0%E5%AD%A6%E7%BF%92%E3%83%97%E3%83%AD%E3%83%95%E3%82%A7%E3%83%83%E3%82%B7%E3%83%A7%E3%83%8A%E3%83%AB%E3%82%B7%E3%83%AA%E3%83%BC%E3%82%BA-%E5%9D%AA%E4%BA%95-%E7%A5%90%E5%A4%AA/dp/4061529242)

> TensorFlow機械学習クックブック Pythonベースの活用レシピ60+</br>
> [amazonで詳細を見る](https://www.amazon.co.jp/TensorFlow%E6%A9%9F%E6%A2%B0%E5%AD%A6%E7%BF%92%E3%82%AF%E3%83%83%E3%82%AF%E3%83%96%E3%83%83%E3%82%AF-Python%E3%83%99%E3%83%BC%E3%82%B9%E3%81%AE%E6%B4%BB%E7%94%A8%E3%83%AC%E3%82%B7%E3%83%9460-impress-top-gear/dp/4295002003?SubscriptionId=AKIAI4N75A3H7VG7SKUQ&amp;tag=cloudstudy09-22&amp;linkCode=xm2&amp;camp=2025&amp;creative=165953&amp;creativeASIN=4295002003)
>> 本書のレビュー記事 :<br> 
>> [【書籍紹介】TensorFlow機械学習クックブック](http://s0sem0y.hatenablog.com/entry/2017/09/08/005322)


---

以下、同様の文献（はてなブログ形式）

<!-- 深層学習: Deep Learning -->
[asin:476490487X:detail]

<!-- 詳解 ディープラーニング ~ TensorFlow・Keras による時系列データ処理 ~-->
[asin:4839962510:detail]

<!-- 深層学習による自然言語処理 (機械学習プロフェッショナルシリーズ) -->
[asin:4061529242:detail]

<!-- TensorFlow機械学習クックブック Pythonベースの活用レシピ60+ -->
[asin:4295002003:detail]
