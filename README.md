
# Prevention and Anonymization of Dox Content on Twitter

<p>This work was done as part of the course IST-597 Fundamentals of Privacy at Penn State.</p>

<p>This repository contains the python code, trained model and the demo of the tool I developed. </p>

Demo 1 - Classification of a Tweet to identify doxing  <br>
Demo 2 - Nudging the user to not post the Tweet that contains sensitive content  <br>
Demo 3 - Anonymizing the Tweet content if the user ignores the nudge.  <br>

<h3>Summary:</h3>
<ol>
    <li> Trained a Machine Learning model for automatic detection of <i>doxed</i> data on Twitter. </li> 
    <li> Developed a nudge-based technology to alert the doxer that the tweet contains private information. </li> 
    <li> Created a prototype that add noise to tweets with <i>doxed </i> information in real-time by implementation of hashing algorithm. </li>
</ol>

<h3>Part I: Detection of <i>doxed</i> content </h3>
We model our problem as a binary classification task, with two classes being <i>doxed</i> tweet and non-doxed/benign tweets.


<p> The results of binary classification task generated using DistilBERT based embeddings. </p>
<img width="289" alt="Screenshot 2023-02-20 at 3 19 32 PM" src="https://user-images.githubusercontent.com/19535724/220211913-e727c9bb-1592-4b5c-a8e1-583e946fc168.png">


<h3>Part II: Real-time Nudging</h3>
<p>We present the prototype of this nudging mechanism in below figures. Figure 1 is the initial prompt from the system, emulating a Twitter platform and containing the text box to curate the tweet. If a tweet is classified as non-doxing, the sequence is terminated. However, if our machine learning model identifies it as a <i>doxed</i> tweet, the author is nudged. Figure 2 displays the nudging message and the text box where the author inputs his/her choice to proceed. Figure 3 shows if the response is <b>N</b>.<p>


<p>The assumed landing page of Twitter.</p>

![prompt1](https://user-images.githubusercontent.com/19535724/220212213-276eb2f0-2cb2-4f53-bcf7-6f6dbdf1810f.png)

<p>The nudge shared with the user to reconsider the content of the tweet </p>

![nudge2_w_policy](https://user-images.githubusercontent.com/19535724/220212240-dcaa1d12-f20d-43bc-9360-3fd5d9dc3290.png)

<p>A response from the system if the user discards the draft.</p>

![response_n](https://user-images.githubusercontent.com/19535724/220212377-a35b151b-53ab-4c25-9119-557bcb3eaa36.png)

<h3>Part III: Data Anonymization</h3>
<p>We anonymize the tweet if the author decides to continue to post it. We leverage regular expressions and spacy's Named Entity Recognition (NER) API. We generate two regexes to extract the IP address and the URLs (We observed that in some cases, the sensitive information is not explicitly written in the tweet but could be accessible through a URL. Therefore, we add noise to URLs as well). We also observed that along with IP address and SSN, tweets contain other types of personal information too (e.g., Full Name, Location Coordinates). Although our model is not trained to detect such PIIs, we attempt to anonymize this sensitive information by a pre-trained NER model provided by Spacy to extract entities. We mask all the entities identified by the NER. </p>

<p>Below figure shows the anonymized response from the system if user discards the nudge. </p>

![response2](https://user-images.githubusercontent.com/19535724/220212467-a0827121-397b-40d5-bf24-a4a4d086294c.png)


Note: Due to privacy concerns, I couldn't share the dataset. The dataset contains user's SSN and IP address information.

PS. More description on methodology coming soon.

