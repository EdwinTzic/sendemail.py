# Send an HTML email with an embedded image and a plain text message for
# email clients that don't want to display the HTML.

from email.MIMEMultipart import MIMEMultipart
from email.MIMEText import MIMEText
from email.MIMEImage import MIMEImage

# Define these once; use them twice!
strFrom = 'edwintzic.yax@gmail.com'
strTo = 'edwintzic.yax@gmail.com'

# Create the root message and fill in the from, to, and subject headers
msgRoot = MIMEMultipart('related')
msgRoot['Subject'] = 'Someone's Here'
msgRoot['From'] = strFrom
msgRoot['To'] = strTo
msgRoot.preamble = 'This is a multi-part message in MIME format.'

# Encapsulate the plain and HTML versions of the message body in an
# 'alternative' part, so message agents can decide which they want to display.
msgAlternative = MIMEMultipart('alternative')
msgRoot.attach(msgAlternative)

msgText = MIMEText('This is the alternative plain text message.')
msgAlternative.attach(msgText)

# This is the message that is attached in the email, that you can customize on your own
# We reference the image in the IMG SRC attribute by the ID we give it below
msgText = MIMEText('<b>New Guest </b> at the door and an <b>Image. </b><br><img src="cid:image1"><br>WOW!', 'html')
msgAlternative.attach(msgText)

# This example assumes the image is in the current directory
fp = open('test.jpg', 'rb')
msgImage = MIMEImage(fp.read())
fp.close()

# Define the image's ID as referenced above
msgImage.add_header('Content-ID', '<image1>')
msgRoot.attach(msgImage)

# This is the only section that I changed from the website
# Send the email (this example assumes SMTP authentication is required)
import smtplib
smtp = smtplib.SMTP(;smtp.gmail.com', 587)
smtp.starttls
smtp.login('strFrom, 'emailpassword')
text = msgRoot.as_string()
smtp.sendmail(strFrom, strTo, msgRoot.as_string())
smtp.quit()
