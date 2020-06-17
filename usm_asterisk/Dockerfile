FROM perl:5

COPY cpanfile /

RUN cpanm --installdeps .

WORKDIR /app

CMD ["perl", "usm_asterisk.pl"]
