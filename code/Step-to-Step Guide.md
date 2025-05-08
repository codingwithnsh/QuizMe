# Step-by-Step Guide: Building the Simple Quiz App in MIT App Inventor

This guide provides instructions on how to construct the Simple Quiz application using MIT App Inventor, based on the provided screenshots and inferred component usage.

## Step 1: Project Setup

1.  Navigate to the MIT App Inventor website (appinventor.mit.edu) and log in.
2.  Click **Projects** > **Start new project**.
3.  Enter a project name (e.g., `SimpleQuizApp`) and click **OK**.

## Step 2: Designing the User Interface (Designer View)

Switch to the **Designer** view.

1.  **Add Quiz Title Image (Optional but shown in UI):**
    * If you have an image like "Quiztime.jpg", upload it in the **Media** section.
    * From the **Palette** > **User Interface**, drag an **`Image`** component onto the Viewer.
    * Select the `Image`. In the **Properties** pane, set its **`Picture`** to your uploaded image file (`Quiztime.jpg`). Adjust `Height` and `Width` as needed.
    * *Optional but Recommended:* Rename to `QuizImage`.

2.  **Add Question Label:**
    * From the **Palette** > **User Interface**, drag a **`Label`** onto the Viewer below the image.
    * Select the `Label`. In Properties, set **`Text`** to `Question:`. Set **`FontBold`** to `true`.
    * *Optional:* Rename to `QuestionLabel`.
    * Drag another **`Label`** below the "Question:" label. This will display the actual question text. Set its initial **`Text`** to something like "Question text goes here" or leave it empty. Set **`Width`** to `Fill parent`.
    * *Optional:* Rename to `QuestionTextLabel`.

3.  **Add Answer Input:**
    * From the **Palette** > **User Interface**, drag a **`Label`** onto the Viewer. Set its **`Text`** to `Answer:`. Set **`FontBold`** to `true`.
    * From the **Palette** > **User Interface**, drag a **`TextBox`** onto the Viewer next to or below the "Answer:" label.
    * Select the `TextBox`. Set **`Width`** to `Fill parent` (or a suitable width). Set **`Hint`** to `Enter your answer here`.
    * *Optional but Recommended:* Rename to `AnswerTextBox`.

4.  **Add Buttons:**
    * From the **Palette** > **Layout**, drag a **`HorizontalArrangement`** onto the Viewer below the answer input.
    * Select the `HorizontalArrangement`. Set **`Width`** to `Fill parent`. Set **`AlignHorizontal`** to `Center`.
    * From the **Palette** > **User Interface**, drag two **`Button`** components into the `HorizontalArrangement`.
    * **Button 1 (Submit):**
        * Select the first `Button`. Set **`Text`** to `Submit`.
        * *Optional:* Rename to `SubmitButton`.
    * **Button 2 (Next):**
        * Select the second `Button`. Set **`Text`** to `Next`.
        * *Optional:* Rename to `NextButton`.

5.  **Add Feedback Label:**
    * From the **Palette** > **User Interface**, drag a **`Label`** onto the Viewer below the buttons.
    * Select the `Label`. Set its initial **`Text`** to `Right/Wrong` (or leave empty). Set **`TextAlignment`** to `Center`. Set **`FontBold`** to `true`.
    * *Optional but Recommended:* Rename to `FeedbackLabel`.

Your Designer view should now contain components similar to the screenshot, although the specific arrangement and sizes might vary.

## Step 3: Programming the App Logic (Blocks Editor)

Click the **Blocks** button in the top right corner to switch to the Blocks Editor.

1.  **Initialize Global Variables (Lists and Index):**
    * Click on **Built-in** > **Variables**. Drag out four **`initialize global name to`** blocks.
    * **Question List:**
        * Rename the first `name` to `QuestionList`.
        * Click on **Built-in** > **Lists**. Drag out a **`make a list`** block.
        * Click on the blue gear icon on the `make a list` block and add as many **`item`** slots as you have questions.
        * Click on **Built-in** > **Text**. Drag out **`text`** blocks and type your questions into them, snapping them into the `item` slots of the list. (e.g., "Which scientist introduced the idea of na..", "A person who studies biology is known as a?", etc., based on the screenshot). Snap the `make a list` block into the `to` socket.
    * **Answer List:**
        * Rename the second `name` to `AnswerList`.
        * Click on **Built-in** > **Lists**. Drag out a **`make a list`** block.
        * Add items for the correct answers corresponding to your questions. Use **`text`** blocks for each answer. (e.g., "Charles Darwin", "Biologist", "Plants", "No", based on the screenshot). Snap the `make a list` block into the `to` socket.
    * **Picture List (Optional):**
        * Rename the third `name` to `picturelist`.
        * Click on **Built-in** > **Lists**. Drag out a **`make a list`** block.
        * Add items for the filenames of images you want to display with each question (e.g., "Quiztime.jpg", "image2.jpg", etc.). Use **`text`** blocks for each filename. Snap the `make a list` block into the `to` socket.
    * **Current Question Index:**
        * Rename the fourth `name` to `currentquestionindex`.
        * Click on **Built-in** > **Math**. Drag out a **`number`** block (with `1`) and snap it into the `to` socket. (Lists in App Inventor are 1-indexed).

2.  **Screen Initialization:**
    * Click on `Screen1`. Drag out the **`when Screen1.Initialize do`** block.
    * Inside this block:
        * Click on `QuestionTextLabel` (or your renamed label). Drag out the **`set QuestionTextLabel.Text to`** block.
        * Click on **Built-in** > **Lists**. Drag out the **`select list item list index`** block.
        * Click on **Built-in** > **Variables**. Drag out the **`get global QuestionList`** block and snap it into the `list` socket.
        * Click on **Built-in** > **Variables**. Drag out the **`get global currentquestionindex`** block and snap it into the `index` socket.

3.  **Submit Button Logic:**
    * Click on `SubmitButton` (or your renamed button). Drag out the **`when SubmitButton.Click do`** block.
    * Inside this block, we need an `if/else` block to check the answer.
    * Click on **Built-in** > **Control**. Drag out an **`if then else`** block.
    * **Condition (Check Answer):**
        * Click on **Built-in** > **Logic**. Drag out the **`=`** comparison block.
        * Click on `AnswerTextBox` (or your renamed textbox). Drag out the **`AnswerTextBox.Text`** block and snap it into the first socket of the `=` block.
        * Click on **Built-in** > **Lists**. Drag out the **`select list item list index`** block.
        * Click on **Built-in** > **Variables**. Drag out the **`get global AnswerList`** block and snap it into the `list` socket.
        * Click on **Built-in** > **Variables**. Drag out the **`get global currentquestionindex`** block and snap it into the `index` socket.
        * Snap the entire `=` block into the `if` condition socket.
    * **If Correct:**
        * Click on `FeedbackLabel` (or your renamed label). Drag out the **`set FeedbackLabel.Text to`** block.
        * Click on **Built-in** > **Text**. Drag out a **`text`** block and type `Correct!! Well done` inside the quotes. Snap it into the `set FeedbackLabel.Text` block.
    * **Else (Incorrect):**
        * Click on `FeedbackLabel`. Drag out the **`set FeedbackLabel.Text to`** block.
        * Click on **Built-in** > **Text**. Drag out a **`text`** block and type `Incorrect!! Try again` inside the quotes. Snap it into the `set FeedbackLabel.Text` block.

4.  **Next Button Logic:**
    * Click on `NextButton` (or your renamed button). Drag out the **`when NextButton.Click do`** block.
    * Inside this block:
        * Clear the feedback and answer text:
            * Click on `FeedbackLabel`. Drag out **`set FeedbackLabel.Text to`**. Use an empty **`text`** block (`""`).
            * Click on `AnswerTextBox`. Drag out **`set AnswerTextBox.Text to`**. Use an empty **`text`** block (`""`).
        * Increment the question index:
            * Click on **Built-in** > **Variables**. Drag out **`set global currentquestionindex to`**.
            * Click on **Built-in** > **Math**. Drag out the **`+`** addition block.
            * Click on **Built-in** > **Variables**. Drag out **`get global currentquestionindex`** and snap it into the first socket of `+`.
            * Click on **Built-in** > **Math**. Drag out a **`number`** block (with `1`) and snap it into the second socket of `+`.
            * Snap the `+` block into the `set global currentquestionindex to` socket.
        * Check if the index is beyond the list length and reset if needed (Looping):
            * Click on **Built-in** > **Control**. Drag out an **`if then`** block.
            * Click on **Built-in** > **Logic**. Drag out the **`=`** comparison block.
            * Click on **Built-in** > **Variables**. Drag out **`get global currentquestionindex`** and snap it into the first socket of `=`.
            * Click on **Built-in** > **Lists**. Drag out the **`length of list`** block.
            * Click on **Built-in** > **Variables**. Drag out **`get global QuestionList`** and snap it into the `list` socket of `length of list`.
            * Snap the `length of list` block into the second socket of the `=` block.
            * Snap the entire `=` block into the `if` condition socket.
            * Inside the `then` part of this `if` block:
                * Click on **Built-in** > **Variables**. Drag out **`set global currentquestionindex to`**.
                * Click on **Built-in** > **Math**. Drag out a **`number`** block (with `1`) and snap it into the `to` socket. (Resets to the first question).
        * Update the Question Label and Image (if using pictures):
            * Click on `QuestionTextLabel`. Drag out **`set QuestionTextLabel.Text to`**.
            * Click on **Built-in** > **Lists**. Drag out **`select list item list index`**.
            * Click on **Built-in** > **Variables**. Drag out **`get global QuestionList`** and snap it into the `list` socket.
            * Click on **Built-in** > **Variables**. Drag out **`get global currentquestionindex`** and snap it into the `index` socket. Snap the `select list item` block into the `set QuestionTextLabel.Text` socket.
            * *If you added an Image component:*
                * Click on `QuizImage` (or your renamed image). Drag out **`set QuizImage.Picture to`**.
                * Click on **Built-in** > **Lists**. Drag out **`select list item list index`**.
                * Click on **Built-in** > **Variables**. Drag out **`get global picturelist`** and snap it into the `list` socket.
                * Click on **Built-in** > **Variables**. Drag out **`get global currentquestionindex`** and snap it into the `index` socket. Snap the `select list item` block into the `set QuizImage.Picture` socket.

Arrange your blocks neatly in the workspace. Your blocks should now look similar to the screenshot provided.

## Step 4: Testing the Application

1.  In the App Inventor web interface, click **Connect** in the top menu.
2.  Choose either "AI Companion" or "Emulator".
3.  Test the application on your device or emulator. Verify that questions change when "Next" is pressed, you can type answers, and the "Submit" button provides correct feedback.

You have successfully built the Simple Quiz application! You can easily customize the quiz by editing the items in the `GlobalQuestionList`, `GlobalAnswerList`, and `GlobalPictureList` blocks.
