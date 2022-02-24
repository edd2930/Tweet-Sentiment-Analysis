punctuation_chars = ["'", '"', ",", ".", "!", ":", ";", "#", "@"]

#function: remove punctuation from tweet
def strip_punctuation(wrd):
    for char in punctuation_chars:
        wrd = wrd.replace(char, "")
    return wrd


# import lists of words to use (positive and negative)
positive_words = []
with open("positive_words.txt") as pos_f:
    for lin in pos_f:
        if lin[0] != ";" and lin[0] != "\n":
            positive_words.append(lin.strip())


negative_words = []
with open("negative_words.txt") as pos_f:
    for lin in pos_f:
        if lin[0] != ";" and lin[0] != "\n":
            negative_words.append(lin.strip())

#function: count positive words
def get_pos(st):
    cnt = 0
    words = st.split()
    for x in words:
        stripped = strip_punctuation(x)
        lwr = stripped.lower()
        if lwr in positive_words:
            cnt += 1
    return cnt

#function: count negative words
def get_neg(st):
    cnt = 0
    words = st.split()
    for x in words:
        stripped = strip_punctuation(x)
        lwr = stripped.lower()
        if lwr in negative_words:
            cnt += 1
    return cnt


# creating output csv file
outfile = open("resulting_data.csv", "w")
# headers
outfile.write(
    "Number of Retweets, Number of Replies, Positive Score, Negative Score, Net Score"
)
outfile.write("\n")

# import tweet csv
fileconnection = open("project_twitter_data.csv", "r")
lines = fileconnection.readlines()
header = lines[0]
field_names = header.strip().split(",")
print(field_names)
for row in lines[1:]:
    vals = row.strip().split(",")
    print("{}: {}; {}".format(vals[0], vals[1], vals[2]))
    # getting positive count for tweet column
    pos = get_pos(vals[0])
    # getting negative count for tweet column
    neg = get_neg(vals[0])
    # net score
    net = pos - neg
    row_string = "{}, {}, {}, {}, {}".format(vals[1], vals[2], pos, neg, net)
    outfile.write(row_string)
    outfile.write("\n")
outfile.close()
