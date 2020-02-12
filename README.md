# Stock-Market-Predictor
A python notebook to analyze and attempt to predict stock market decisions using tensorflow

I use stock market data sourced from yahoo finance of the opening, high, and low prices of the S&P 500 and Walmart. Using the Walmart data, I then inspect the data, format it, and calculate metrics to suggest buy and sell levels. I then train a convolutional neural net (created in Tensorflow) on this data in an attempt to predict whether I should buy or sell given previous data.

To generate the buy/sell data, I looked 70 days into the future, in growing chunks. So, in the week ahead, I used each day, 2 days were grouped together, then 5, then I had two groups of 15 days. Then, for each of these date ranges I calculated the absolute highest and absolute lowest value. When comparing the current (opening) price to this range, I could check to see if it was inside the range or not. Being outside the range indicated a guaranteed gain/loss, and so only if it was outside of the range would the values change. If the value was above the range, this meant our stock price would likely fall and we should sell. If it was below the range, the stock price was likely to rise, and we should buy. The exact amount was just the distance to the center of the range, since this allowed larger ranges to also convey possibilities of larger changes. They are also scaled down by the current price, so all changes are relative and not dependent on actual price, but rather percent change.

After that, I smoothed these values a little, so they ranged from 0 to 1, with approximately a uniform distribution. This could then be graphed  and makes a really pretty graph of choices.

I then prepped my data (both in limiting x, and in scaling the y) and my tensorflow model. I used a convolutional nerual net with 3 convolutions (all with kernels of 9, one with 10 filters, 20, and 30), three layer of 20 neurons, and then the 2 neurons for the output layer. I trained it for 15 epochs on 11,337 business days each.

The results were dissapointing though. The model didn't make any predictions, instead opting to leave both buy and sell likelihoods at 0. I'm guessing that this is because the stock market is too random (well, actually is more reliant on other factors than previous price points), so it is difficult for the model to actually find any patterns. Anything it learned for one was likely unlearned for the next value. 

But, I still had a great time making it and learned a lot in the process.

As a note, the notebook is viewable in github (albeit with some weird bugs). But, if you would like to download and modify it for yourself, feel free, you just need to have some form of jupyter notebook in order to be able to read the .ipynb file. I use Anaconda on my laptop, but there are certainly online viewers available as well.
