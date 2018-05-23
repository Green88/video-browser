<template>
    <div class="container">
        <SearchBar @termChange="onTermChange" />
        <div class="row">
            <VideoDetail :video="video"></VideoDetail>
            <VideoList :videos="videos"  @videoSelect="onVideoSelect"></VideoList>
        </div>
    </div>
</template>

<script>
    import axios from 'axios';
    import SearchBar from './components/SearchBar';
    import VideoList from './components/VideoList';
    import VideoDetail from './components/VideoDetail';
    import { YOUTUBE_API_KEY } from '../constants';
    import { YOUTUBE_ENDPOINT } from '../constants';

    export default {
        name: "App",
        components: {
            VideoDetail,
            VideoList,
            SearchBar
        },
        data: function() {
            return {
                videos: [],
                video: null
            };
        },
        methods: {
            onTermChange: function(searchTerm) {
                axios.get(YOUTUBE_ENDPOINT, {
                    params: {
                        key: YOUTUBE_API_KEY,
                        type: 'video',
                        part: 'snippet',
                        q: searchTerm
                    }
                }).then(response => {
                    this.videos = response.data.items;
                });
            },
            onVideoSelect: function(video) {
                // eslint-disable-next-line
                console.log(video);
                this.video = video;
            }
        }
    }
</script>