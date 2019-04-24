FROM nginx:1.15.12-alpine

RUN apk add git yarn
RUN git clone https://github.com/bfh-proj1-sumfrie/frontend.git
RUN cd frontend && git fetch --tags && \
    latestTag=$(git describe --tags `git rev-list --tags --max-count=1`) && \
    git checkout $latestTag && yarn install && yarn build
RUN rm /usr/share/nginx/html/index.html && rm /usr/share/nginx/html/50x.html
RUN ls -al  /usr/share/nginx
RUN mv frontend/dist/* /usr/share/nginx/html
RUN ls -al  /usr/share/nginx/html